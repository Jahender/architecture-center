**Secure Azure Computing Architecture**

**[Executive Summary]{.underline}** -- A rapidly increasing number of
DoD customers deploying workloads to Azure have been asking for guidance
setting up secure virtual networks and configuring the security tools
and services stipulated by DoD standards and practice. DISA published
the Secure Cloud Computing Architecture (SCCA) functional requirements
document in 2017. SCCA describes the functional objectives for securing
the Defense Information System Network's (DISN) and Commercial Cloud
Provider connection points and how mission owners secure cloud
applications at the connection boundary. It is mandated that every DoD
entity that connects to the commercial cloud follows the guidelines set
forth in the SCCA FRD.

There are four components of the SCCA. The Boundary Cloud Access Point
(BCAP), Virtual Datacenter Security Stack (VDSS), Virtual Datacenter
Services (VDMS), and Trusted Cloud Credential Manager (TCCM). Microsoft
has developed a solution that will meet the SCCA requirements for both
IL4 and IL5 workloads running in Azure. This Azure specific solution is
called Secure Azure Computing Architecture (SACA). Customers who deploy
SACA will be in compliance with the SCCA FRD and will enable DoD
customers to move workloads into Azure once connected.

While SCCA guidance and architectures are specific to DoD customers, the
latest revisions to SACA will also help Civilian customers comply with
trusted internet connection (TIC) guidance, as well as commercial
customers that with to implement a secure DMZ to protect their azure
environments.

**Secure Cloud Computing Architecture Components**

**BCAP**

The purpose of the BCAP is to protect the DISN from attacks originating
in the cloud environment. BCAP will perform intrusion detection and
prevention as well as filter out unauthorized traffic. This component
can be co-located with other components of the SCCA. It is highly
recommended that this component is deployed using physical hardware.
Below you will find the list of BCAP security requirements.

  ***Req. ID***   **BCAP Security Requirements**
  ------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  2.1.1.1.1     The BCAP shall provide the capability to detect and prevent malicious code injection into the DISN originating from the CSE
  2.1.1.1.2     The BCAP shall provide the capability to detect and thwart single and multiple node DOS attacks
  2.1.1.1.3     The BCAP shall provide the ability to perform detection and prevention of traffic flow having unauthorized source and destination IP addresses, protocols, and Transmission Control Protocol (TCP)/User Datagram Protocol (UDP) ports
  2.1.1.1.4     The BCAP shall provide the capability to detect and prevent IP Address Spoofing and IP Route Hijacking
  2.1.1.1.5     The BCAP shall provide the capability to prevent device identity policy infringement (prevent rogue device access)
  2.1.1.1.6     The BCAP shall provide the capability to detect and prevent passive and active network enumeration scanning originating from within the CSE
  2.1.1.1.7     The BCAP shall provide the capability to detect and prevent unauthorized data exfiltration from the DISN to an endpoint inside CSE
  2.1.1.1.8     The BCAP and/or BCAP Management System shall provide the capability to sense, correlate, and warn on advanced persistent threats
  2.1.1.1.9     The BCAP shall provide the capability to detect custom traffic and activity signatures
  2.1.1.1.10    The BCAP shall provide an interface to conduct ports, protocols, and service management (PPSM) activities in order to provide control for BCND provider
  2.1.1.1.11    The BCAP shall provide full packet capture (FPC) for traversing communications
  2.1.1.1.12    The BCAP shall provide network packet flow metrics and statistics for all traversing communications
  2.1.1.1.13    The BCAP shall provide the capability to detect and prevent application session hijacking

**VDSS**

The purpose of the VDSS is to protect DoD Mission Owner applications
that are hosted in Azure. VDSS performs the bulk of the security
operations in the SCCA. It will conduct traffic inspection in order to
secure the applications running in Azure. This component can be provided
within your Azure environment.

  **Req. ID**   **VDSS Security Requirements**
  ------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  2.1.2.1       The VDSS shall maintain virtual separation of all management, user, and data traffic
  2.1.2.2       The VDSS shall allow the use of encryption for segmentation of management traffic.
  2.1.2.3       The VDSS shall provide a reverse proxy capability to handle access requests from client systems
  2.1.2.4       The VDSS shall provide a capability to inspect and filter application layer conversations based on a predefined set of rules (including HTTP) to identify and block malicious content
  2.1.2.5       The VDSS shall provide a capability that can distinguish and block unauthorized application layer traffic
  2.1.2.6       The VDSS shall provide a capability that monitors network and system activities to detect and report malicious activities for traffic entering and exiting Mission Owner virtual private networks/enclaves
  2.1.2.7       The VDSS shall provide a capability that monitors network and system activities to stop or block detected malicious activity
  2.1.2.8       The VDSS shall inspect and filter traffic traversing between mission owner virtual private networks/enclaves.
  2.1.2.9       The VDSS shall perform break and inspection of SSL/TLS communication traffic supporting single and dual authentication for traffic destined to systems hosted within the CSE12.
  2.1.2.10      The VDSS shall provide an interface to conduct ports, protocols, and service management (PPSM) activities in order to provide control for MCD operators
  2.1.2.11      The VDSS shall provide a monitoring capability that captures log files and event data for cybersecurity analysis
  2.1.2.12      The VDSS shall provide or feed security information and event data to an allocated archiving system for common collection, storage, and access to event logs by privileged users performing Boundary and Mission CND activities
  2.1.2.13      The VDSS shall provide a FIPS-140-2 compliant encryption key management system for storage of DoD generated and assigned server private encryption key credentials for access and use by the Web Application Firewall (WAF) in the execution of SSL/TLS break and inspection of encrypted communication sessions.
  2.1.2.14      The VDSS shall provide the capability to detect and identify application session hijacking
  2.1.2.15      The VDSS shall provide a DoD DMZ Extension to support to support Internet Facing Applications (IFAs)
  2.1.2.16      The VDSS shall provide full packet capture (FPC) or cloud service equivalent FPC capability for recording and interpreting traversing communication
  2.1.2.17      The VDSS shall provide network packet flow metrics and statistics for all traversing communications
  2.1.2.18      The VDSS shall provide for the inspection of traffic entering and exiting each mission owner virtual private network.

**VDMS**

The purpose of VDMS is to provide host security as well as shared data
center services. The functions of VDMS can either run in the hub of your
SCCA or the mission owner can deploy pieces of it in their own specific
Azure subscription. This component can be provided within your Azure
environment.

  **Req. ID**   **VDMS Security Requirements**
  ------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  2.1.3.1       The VDMS shall provide Assured Compliance Assessment Solution (ACAS), or approved equivalent, to conduct continuous monitoring for all enclaves within the CSE
  2.1.3.2       The VDMS shall provide Host Based Security System (HBSS), or approved equivalent, to manage endpoint security for all enclaves within the CSE
  2.1.3.3       The VDMS shall provide identity services to include an Online Certificate Status Protocol (OCSP) responder for remote system DoD Common Access Card (CAC) two-factor authentication of DoD privileged users to systems instantiated within the CSE
  2.1.3.4       The VDMS shall provide a configuration and update management system to serve systems and applications for all enclaves within the CSE
  2.1.3.5       The VDMS shall provide logical domain services to include directory access, directory federation, Dynamic Host Configuration Protocol (DHCP), and Domain Name System (DNS) for all enclaves within the CSE
  2.1.3.6       The VDMS shall provide a network for managing systems and applications within the CSE that is logically separate from the user and data networks
  2.1.3.7       The VDMS shall provide a system, security, application, and user activity event logging and archiving system for common collection, storage, and access to event logs by privileged users performing BCP and MCP activities.
  2.1.3.8       The VDMS shall provide for the exchange of DoD privileged user authentication and authorization attributes with the CSP\'s Identity and access management system to enable cloud system provisioning, deployment, and configuration
  2.1.3.9       The VDMS shall implement the technical capabilities necessary to execute the mission and objectives of the TCCM role.

**TCCM**

TCCM is a business role. This individual will be responsible for
managing the SCCA. Their duties include establishing plans and policies
for account access to the cloud environment, ensuring identity and
access management is operating properly, and to maintain the Cloud
Credential Management Plan. This individual is appointed by the
Authorizing Official. The BCAP, VDSS, and VDMS will provide the
capabilities needed for the TCCM to perform their job function.

  **Req. ID**   **TCCM Security Requirements**
  ------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  2.1.4.1       The TCCM shall develop and maintain a Cloud Credential Management Plan (CCMP) to address the implementation of policies, plans, and procedures that will be applied to mission owner customer portal account credential management
  2.1.4.2       The TCCM shall collect, audit, and archive all Customer Portal activity logs and alerts
  2.1.4.3       The TCCM shall ensure activity log alerts are shared with, forwarded to, or retrievable by DoD privileged users engaged in MCP and BCP activities
  2.1.4.4       The TCCM shall, as necessary for information sharing, create log repository access accounts for access to activity log data by privileged users performing both MCP and BCP activities
  2.1.4.5       The TCCM shall recover and securely control customer portal account credentials prior to mission application connectivity to the DISN
  2.1.4.6       The TCCM shall create, issue, and revoke, as necessary, role-based access least privileged customer portal credentials to mission owner application and system administrators (i.e., DoD privileged users).
  2.1.4.7       The TCCM shall limit, to the greatest extent possible, the issuance of customer portal and other CSP service (e.g., API, CLI) end-point privileges to configure network, application, and CSO elements
  2.1.4.8       The TCCM shall ensure that privileged users are not allowed to use CSP IdAM derived credentials which possess the ability to unilaterally create unauthorized network connections within the CSE, between the CSO and the CSP's private network, or to the Internet

**SACA Components and Planning Considerations**

**The SACA reference architecture is designed to deploy the VDSS and
VDMS components in azure, as well as enable the TCCM. This architecture
is modular, which means that all of the pieces of VDSS and VDMS can live
in a centralized hub or some of the controls can be met in the mission
owner space or even on-premises. The recommendation of our Microsoft
team is to co-locate the VDSS and VDMS components into a central Virtual
Net that all Mission Owners can connect through. The diagram below
depicts our recommended architecture.**

![A close up of a map Description automatically
generated](media/image1.jpg)

When planning your SCCA compliancy strategy and technical architecture,
there are many things to consider. It is important that the following
topics are taken into consideration from the beginning, as every
customer will need to cover these. The topics below have been issues
that have come up with real DoD customers and tend to slow the planning
and execution down.

-   Which BCAP will your organization use?

    -   DISA BCAP

        -   DISA has two operational BCAPs at the Pentagon, and Camp
            Roberts CA, with a third coming online soon.

        -   DISA's BCAPs all have ExpressRoute circuits to Azure, which
            can be leveraged by DoD customers for connectivity.

        -   DISA already has an enterprise level Microsoft Peering
            session for DoD customers who want to subscribe to Microsoft
            SaaS tools, such as Office 365. By using DISA BCAP, you can
            enable connectivity and peering to your SACA instance.

    -   Build your own BCAP

        -   This would require you to lease space in a co-located data
            center and setup an ExpressRoute circuit to Azure.

        -   This option will require additional approval

        -   Due to additional approval and a physical build out, this
            option takes the most time.

    -   Microsoft's recommendation is to utilize the DISA BCAP. This
        option is readily available, has built in redundancy, and
        already has customers operating on it today in production.

-   DoD routable IP space

    -   You will be required to use DoD routable IP space at your edge.
        The option to NAT those to private IP space in Azure is
        available.

    -   Contact DoD NIC to obtain IP space, it will be needed as part of
        your SNAP submission with DISA.

    -   If you plan to NAT to private address space in Azure, you will
        need a minimum of a /24 subnet of address space assigned from
        the NIC for each region you plan to deploy SACA.

-   Redundancy

    -   Microsoft suggests that you deploy a SACA instance to at least
        two regions. In DoD cloud this would mean you deploy it to both
        available DoD regions.

    -   It is also suggested that you connect to at least two BCAPs via
        separate ExpressRoute circuits. Both Express Routes can then be
        linked to each region's SACA instance.

-   DoD component specific requirements

    -   Does your organization have any specific requirements outside
        the SCCA requirements? (Some organizations have specific IPS
        requirements)

-   SACA is a modular architecture

    -   Use only which components you need for your environment.

        -   Deploy NVAs in a single tier or multi-tier

        -   Integrated IPS, or bring your own IPS

-   DoD impact level of your applications and data

    -   If there is any possibility of applications running in our IL5
        regions, it is suggested that you build your SACA instance in
        IL5. The instance can be used in front of IL4 applications as
        well as IL5. But, an IL4 SACA instance in front of an IL5
        application will most likely not receive accreditation.

-   Which Network Virtual Appliance vendor will you use for VDSS?

    -   As mentioned earlier, this SACA reference can be built using a
        variety of appliances and Azure services. However, we do have
        automated solution templates to deploy the SACA architecture
        with both F5 and Citrix. These solutions will be covered in more
        detail below.

-   Which Azure services will you use?

    -   There are Azure services that can meet requirements around log
        analytics, host-based protection, and IDS functionality.
        However, it is possible that some services aren't generally
        available in our IL5 regions. This may lead to the need to use
        some 3^rd^ party tools if these Azure services can't meet your
        requirement. You will need to look at what tools you are
        comfortable with and the feasibility of using Azure native
        tooling.

    -   It is Microsoft's recommendation that you use as many Azure
        native tools as possible as they are all built with cloud
        security in mind and seamlessly integrate with the rest of the
        Azure platform. Below is a list of Azure native tools that can
        be leveraged to meet various requirements of SCCA.

        -   Azure Monitor -
            <https://docs.microsoft.com/en-us/azure/azure-monitor/overview>

        -   Azure Security Center -
            <https://docs.microsoft.com/en-us/azure/security-center/security-center-intro>

        -   Network Watcher -
            <https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview>

        -   Azure Key Vault -
            <https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis>

        -   Azure Active Directory -
            <https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/active-directory-whatis>

        -   Application Gateway -
            <https://docs.microsoft.com/en-us/azure/application-gateway/overview>

        -   Azure Firewall -
            <https://docs.microsoft.com/en-us/azure/firewall/overview>

        -   Azure Front Door -
            <https://docs.microsoft.com/en-us/azure/frontdoor/front-door-overview>

        -   Security Groups -
            <https://docs.microsoft.com/en-us/azure/virtual-network/security-overview>

        -   Azure DDoS Protection -
            <https://docs.microsoft.com/en-us/azure/virtual-network/ddos-protection-overview>

        -   Azure Sentinel-
            <https://docs.microsoft.com/en-us/azure/sentinel/overview>

-   Sizing

    -   A sizing exercise will need to be completed. You will need to
        look at the amount of concurrent connections you may have
        through the SACA instance as well as the network throughput
        requirements.

    -   This is a critical step as it will help to size the VMs, as well
        as help to identify the licenses that will be required from the
        various vendors you will be using in your SACA instance.

    -   A good cost analysis can't be done without this sizing exercise,
        it is also important to ensure everything is sized correctly to
        allow for best performance.

**Most Common Deployment Scenario**

Microsoft has several customers who have already gone through the full
deployment or at least planning stages of their SACA environments. This
has allowed us to get insight into the most common deployment scenario.
The diagram below depicts the most common architecture.

![A close up of a device Description automatically
generated](media/image2.jpg)

As you can see from the diagram, DoD customers typically subscribe to
two of the DISA BCAPs, one of these lives on the west coast and the
other lives on the east coast. An ExpressRoute Private peer is enabled
to Azure at each DISA BCAP location. These ExpressRoute Peers are then
linked to the Virtual Network Gateway in the DoD East and DoD Central
Azure Regions. A SACA instance is deployed in the DoD East and DoD
Central Azure region and all ingress and egress traffic flows through it
to and from the Express Route connection to the DISA BCAP.

Mission Owner applications then choose which Azure region(s) they will
deploy their applications in and use Virtual Network Peering to connect
their application's Virtual Network to the SACA Virtual Network. Force
Tunneling all their traffic through the VDSS instance.

This architecture is highly recommended by Microsoft, as it will meet
SCCA requirements, it's highly available, easily scalable, and it
simplifies deployment and management.

**Automated SACA deployment Options**

Earlier we mentioned that Microsoft has partnered with two vendors to
create an automated SACA infrastructure template. Both templates will
deploy the following Azure components.

-   SACA Virtual Network

    -   Management Subnet

        -   Where management VMs and services are deployed (jump boxes)

    -   VDMS Subnet

        -   Where VMs and services used for VDMS are deployed

    -   Untrusted and Trusted Subnets

        -   Where virtual appliances are deployed

    -   Gateway Subnet

        -   Where the ExpressRoute Gateway will be deployed

-   Management Jump Box Virtual Machines

    -   Used for Out of Band Management of the environment

-   Network Virtual Appliances

-   Public IPs

    -   Used for front end until ExpressRoute is brought online. These
        IPs will translate to the backend Azure private address space

-   Route Tables

    -   Applied during automation, these route tables force-tunnel all
        traffic through the virtual appliances

-   Azure Load Balancers - Standard SKU

    -   These are used to load balance traffic across the appliances

Citrix SACA Deployment

Citrix has created a deployment template that deploys two layers of
highly available Citrix ADC appliances. This architecture meets the
requirements of VDSS.

![](media/image3.png)

Citrix Documentation and deployment script can be found here -
<https://github.com/citrix/netscaler-azure-templates/tree/master/templates/saca>

F5 SACA Deployment

F5 has created two separate deployment templates covering two different
architectures. The first one has only one layer of F5 appliances in an
active-active highly available configuration. This architecture meets
the requirements for VDSS. The second adds a second layer of
active-active highly available F5s. The purpose of this second layer is
to allow for customers to add their own IPS separate from F5 in between
the F5 layers. Not all DoD components have specific IPS prescribed for
use. If that is the case, the single layer of F5 appliances will work
for most since that architecture includes IPS on the F5 devices.

![](media/image4.png)

F5 Documentation and deployment script can be found here -
<https://github.com/f5devcentral/f5-azure-saca>

**SACA Support**

**If you have questions about SACA please reach out to ALIAS HERE**

**Learn More About Azure Government**

Microsoft is committed to providing the most trusted, comprehensive
cloud for mission-critical workloads so that our nearly 6 million
government users across 7,000-plus federal, state, and local
organizations can achieve more in carrying out their mission-critical
workloads.

We welcome your comments and suggestions to help us continually improve
your Azure Government experience. To stay up to date on all things Azure
Government, click "Subscribe by Email!" on the [Azure Government
Blog](https://devblogs.microsoft.com/azuregov/). To explore Azure
Government, [request your free 90-day trial
today](https://azure.microsoft.com/en-us/overview/clouds/government/request/).
Or, check out purchasing options to [get started
now](https://azure.microsoft.com/en-us/offers/azure-government/).
