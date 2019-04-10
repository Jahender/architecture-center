---
# This basic template provides core metadata fields for Markdown articles on docs.microsoft.com.

# Mandatory fields.
title: Secure Azure Computing Architecture
description: This is a reference architecture for an enterprise level DMZ architecture, utilizing Network Virtual Appliances and other tools. This architecture was designed to meet the Department of Defense's Secure Cloud Computing Architecture Functional Requirements. However, it can be leveraged for any organization. This reference inlcudes two automated options using Citrix or F5 appliances.
author: Jason Henderson
ms.author: jahender # Microsoft employees only
ms.date: 4/9/2019
ms.topic: article-type-from-white-list
# Use ms.service for services or ms.prod for on-prem products. Remove the # before the relevant field.
# ms.service: service-name-from-white-list
# ms.prod: product-name-from-white-list

# Optional fields. Don't forget to remove # if you need a field.
# ms.custom: can-be-multiple-comma-separated
# ms.reviewer: MSFT-alias-of-reviewer
# manager: MSFT-alias-of-manager-or-PM-counterpart
---
# Secure Azure Computing Architecture

A rapidly increasing number of DoD customers deploying workloads to Azure have been asking for guidance setting up secure virtual networks and configuring the security tools and services stipulated by DoD standards and practice. DISA published the Secure Cloud Computing Architecture (SCCA) functional requirements document in 2017. SCCA describes the functional objectives for securing the Defense Information System Network’s (DISN) and Commercial Cloud Provider connection points and how mission owners secure cloud applications at the connection boundary. It is mandated that every DoD entity that connects to the commercial cloud follows the guidelines set forth in the SCCA FRD.
 
There are four components of the SCCA. The Boundary Cloud Access Point (BCAP), Virtual Datacenter Security Stack (VDSS), Virtual Datacenter Services (VDMS), and Trusted Cloud Credential Manager (TCCM). Microsoft has developed a solution that will meet the SCCA requirements for both IL4 and IL5 workloads running in Azure. This Azure specific solution is called Secure Azure Computing Architecture (SACA). Customers who deploy SACA will be in compliance with the SCCA FRD and will enable DoD customers to move workloads into Azure once connected. 

While SCCA guidance and architectures are specific to DoD customers, the latest revisions to SACA will also help Civilian customers comply with trusted internet connection (TIC)guidance, as well as commercial customers that with to implement a secure DMZ to protect their azure environments. 


## Secure Cloud Computing Architecture Components


