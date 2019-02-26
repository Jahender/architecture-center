---
title: Monitoring Azure Databricks in Azure Log Analytics
titleSuffix: A solution for monitoring Azure Databricks in Azure Log Analytics
description: A scala library to deploy to a Databricks cluster to enable monitoring of metrics and logging data in Azure Log Analytics
author: petertaylor9999
ms.date: 01/28/2019
ms.topic:
ms.service:
ms.subservice:
---

# Monitoring Azure Databricks in Azure Log Analytics

[Azure Databricks](/azure/azure-databricks/) is a fast, powerful, and collaborative [Apache Spark](https://spark.apache.org/)–based analytics service that makes it easy to rapidly develop and deploy big data analytics and artificial intelligence (AI) solutions. Most users take advantage of the simplicity of notebooks in their Azure Databricks solutions. For users that require more robust computing options, Azure Databricks supports the distributed execution of custom application code written in Scala.

Monitoring in custom application code is a critical part of any production-level solution, and Azure Databricks offers robust functionality for monitoring custom application metrics, streaming query event information, and application log messages. Azure Databricks supports delivery of metrics and logging data to many different logging services, and the code library that accompanies this document extends the core monitoring functionality of Azure Databricks to send streaming query event information to Azure Log Analytics.

The audience for this document and accompanying code library are advanced Apache Spark and Azure Databricks solution developers. The code must be built into Java Archive (JAR) files and then deployed to an Azure Databricks cluster using the [Azure Databricks file system](https://docs.azuredatabricks.net/user-guide/dbfs-databricks-file-system.html) and a [cluster node initilization script](https://docs.azuredatabricks.net/user-guide/clusters/init-scripts.html). The code is a combination of [Scala](https://www.scala-lang.org/) and Java, with a corresponding set of [Maven](https://maven.apache.org) project object model (POM) files to build the output JAR files. An advanced understanding of Java, Scala, and Maven are recommended as prerequisistes.

## About the Azure Databricks monitoring library

The library that accompanies this document is available from the [Spark monitoring Github repository](https://github.com/mspnp/spark-monitoring). The repository has the following directory structure:

/src
&nbsp;&nbsp;/spark-jobs
&nbsp;&nbsp;/spark-listeners-loganalytics
&nbsp;&nbsp;/spark-listeners
&nbsp;&nbsp;/pom.xml

The **spark-jobs** directory is a sample Spark application with sample code demonstrating how to implement a Spark application metric counter.

The **spark-listeners-loganalytics** and **spark-listeners** directories contain the code for building the two JAR files that are deployed to the Databricks cluster. The **spark-listeners** directory includes a **scripts** directory that contains a cluster node initialization script to copy the JAR files from a staging directory in the Azure Databricks file system to execution nodes.

The **pom.xml** file is the main Maven project object model build file for the entire project.

## Build the Azure Databricks monitoring library and configure an Azure Databricks cluster

Integration of the code library accompanying this document into your application has the following prerequisites:

* Clone, fork, or download the [GitHub repository](https://github.com/mspnp/spark-monitoring).
* An active Azure Databricks workspace. For instructions on how to deploy an Azure Databricks workspace, see [get started with Azure Databricks.](https://docs.microsoft.com/azure/azure-databricks/quickstart-create-databricks-workspace-portal).
* Install the [Azure Databricks CLI](https://docs.databricks.com/user-guide/dev-tools/databricks-cli.html#install-the-cli).
  * An Azure Databricks personal access token is required to use the CLI. For instructions, see [token management](https://docs.azuredatabricks.net/api/latest/authentication.html#token-management).
  * You can also use the Azure Databricks CLI from the Azure Cloud Shell.
* A Java IDE, with the following resources:
  * [Java Devlopment Kit (JDK) version 1.8](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
  * [Scala language SDK 2.11](https://www.scala-lang.org/download/)
  * [Apache Maven 3.5.4](http://maven.apache.org/download.cgi)

### Build the Azure Databricks monitoring library

To build the Azure Databricks monitoring library, follow these steps:

1. Import the Maven project project object model file, _pom.xml_, located in the **/src** folder into your project. This will import three projects:

* spark-jobs
* spark-listeners
* spark-listeners-loganalytics

2. Execute the Maven **package** build phase in your Java IDE to build the JAR files for each of the these three projects:

|Project| JAR file|
|-------|---------|
|spark-jobs|spark-jobs-1.0-SNAPSHOT.jar|
|spark-listeners|spark-listeners-1.0-SNAPSHOT.jar|
|spark-listeners-loganalytics|spark-listeners-loganalytics-1.0-SNAPSHOT.jar|

3. Use the Azure Databricks CLI to create a directory named **dbfs:/databricks/monitoring-staging**:  

  ```bash
  dbfs mkdirs dbfs:/databricks/monitoring-staging
  ```

4. Use the Azure Databricks CLI to copy **/src/spark-listeners/scripts/listeners.sh** to the directory created in step 3:

```bash
dbfs cp <local path to listeners.sh> dbfs:/databricks/monitoring-staging/listeners.sh
```

5. Use the Azure Databricks CLI to copy **/src/spark-listeners/scripts/metrics.properties** to the directory created in step 3:

```bash
dbfs cp <local path to metrics.properties> dbfs:/databricks/monitoring-staging/metrics.properties
```

6. Use the Azure Databricks CLI to copy **spark-listeners-1.0-SNAPSHOT.jar** and **spark-listeners-loganalytics-1.0-SNAPSHOT.jar** that were built in step 2 to the directory created in step 3:

```bash
dbfs cp <local path to spark-listeners-1.0-SNAPSNOT.jar> dbfs:/databricks/monitoring-staging/spark-listeners-1.0-SNAPSHOT.jar
dbfs cp <local path to spark-listeners-loganalytics-1.0-SNAPSHOT.jar> dbfs:/databricks/monitoring-staging/spark-listeners-loganalytics-1.0-SNAPSHOT.jar
```

### Create and configure the Azure Databricks cluster

To create and configure the Azure Databricks cluster, follow these steps:

1. Navigate to your Azure Databricks workspace in the Azure Portal.
2. On the home page, click "new cluster".
3. Choose a name for your cluster and enter it in "cluster name" text box. 
4. In the "Databricks Runtime Version" dropdown, select **4.3 (includes Apache Spark 2.3.1, Scala 2.11)**.
5. Under "Advanced Options", click on the "Spark" tab. Enter the following name-value pairs in the "Spark Config" text box:

| Name | Value |
|-------|--------|
|spark.extraListeners|com.databricks.backend.daemon.driver.DBCEventLoggingListener,org.apache.spark.listeners.UnifiedSparkListener|
|spark.unifiedListener.sink |org.apache.spark.listeners.sink.loganalytics.LogAnalyticsListenerSink|
|spark.unifiedListener.logBlockUpdates|false|

6. While still under the "Spark" tab, enter the following in the "Environment Variables" text box:
* LOG_ANALYTICS_WORKSPACE_ID=[your Azure Log Analytics workspace ID](/azure/azure-monitor/platform/agent-windows#obtain-workspace-id-and-key)
* LOG_ANALYTICS_WORKSPACE_KEY=[your Azure Log Analytics shared access signature](/azure/azure-monitor/platform/agent-windows#obtain-workspace-id-and-key)
7. While still under the "Advanced Options" section, click on the "Init Scripts" tab. Go to the last line under the "Init Scripts section" Under the "destination" dropdown, select "DBFS". Enter "dbfs:/databricks/monitoring-staging/listeners.sh" in the text box. Click the "add" button.
8. Click the "create cluster" button to create the cluster. Next, click on the "start" button to start the cluster.

### Monitor your Azure Databricks cluster

Once you have completed all the steps above, your Databricks cluster streams some metric data about the cluster itself to your Azure Log Analytics workspace. This log data is available in your Azure Log Analytics workspace under the "Active" "Custom Logs" "SparkMetric_CL" namespace.

Spark Structured Streaming event data from Azure Databricks also streams to your Azure Log Analytics workspace. This log data is available under the "Active", "Custom Logs", "SparkListenerEvent_CL" schema.

## Monitoring Apache Spark Structured Streaming queries in Azure Databricks

Azure Databricks is a service based on Apache Spark, which includes a set of structured APIs for batch processing data using Datasets, DataFrames, and SQL. With Apache Spark 2.0, support was added for [Structured Streaming](https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html), a data stream processing API built upon Spark's batch processing APIs.

The Structured Streaming API enables you to monitor active streams by sending event information to an external metrics system. By following the instructions in the previous section, Structured Streaming event information is sent to your Azure Log Analytics workspace. 

## Next steps

Learn more about [Structured Streaming](https://docs.databricks.com/spark/latest/structured-streaming/index.html) in Azure Databricks.