---

copyright:
  years: 2025
lastupdated: "2025-06-30"

keywords: HA for transit gateway, DR for transit gateway, transit gateway recovery time objective, transit gateway recovery point objective

subcollection: transit gateway

---

{{site.data.keyword.attribute-definition-list}}

# Understanding high availability and disaster recovery for {{site.data.keyword.tg_full_notm}}
{: #ha-dr-transit-gateway}

[High availability](#x2284708){: term} (HA) is the ability for a service to remain operational and accessible in the presence of unexpected failures. [Disaster recovery](#x2113280){: term} (DR) is the process of recovering the service instance to a working state.
{: shortdesc}

IBM Cloud Transit Gateway is a highly available service designed to meet the [Service Level Objectives (SLO)](/docs/resiliency?topic=resiliency-slo#slo-high-network-services). It is a regional service built on a resilient, distributed infrastructure and supports connectivity across multiple zones within a region. Transit Gateway enables seamless communication between IBM Cloud resources, such as Virtual Private Clouds (VPCs), and supports highly available network architectures through redundant connections and automatic route propagation.

You are responsible for understanding your configuration, customization, and usage of the service. You are also responsible for being ready to recreate an instance of the service in a new region and restore your data in a new region.
{: important}

To better understand the underlying infrastructure, including definitions of data centers and zones, see [IBM Cloud region and data center locations for resource deployment](/docs/overview?topic=overview-locations), which details how zones map to physical data centers. For information about available regions and data center locations for Transit Gateway, see [Transit Gateway locations](/docs/transit-gateway?topic=transit-gateway-tg-locations).

## High availability architecture
{: #ha-architecture}

IBM Cloud Transit Gateway is a regional, highly available service built on Multi-Zone Regions (MZRs), offering a 99.99% SLA with no single point of failure within a region. When you create a Transit Gateway, it is automatically deployed across multiple availability zones, each located in a distinct physical facility, ensuring resilience against zone-level failures.

Transit Gateway ensures that traffic remains within its originating zone when possible. In the event of a zonal outage, traffic is transparently rerouted through the remaining zones, maintaining uninterrupted connectivity across your IBM Cloud environment.

For GRE tunnel-based connections, which are single-threaded by default, high availability requires explicit redundancy. When you configure a GRE connection on a Transit Gateway, you must specify the availability zone. To meet high availability needs, use a Redundant GRE configuration with at least two tunnels, or configure multiple GRE connections across different availability zones.

GRE connections require the gateway owner to configure high availability based on their specific requirements.
{: note}

While Transit Gateway supports global routing to link multiple regions, it does not automatically replicate configuration or state across regional instances. To protect against full-region outages, deploy a mirrored Transit Gateway in a secondary region, replicate your attachments and routing configurations, and plan failover mechanisms accordingly.

IBM Cloud regions that support Transit Gateway are multi-zone regions except for Montreal, which is a single-zone region. In Montreal, Transit Gateway does not offer zone-level redundancy. If deploying in this region, be sure to implement additional measures, such as a mirrored transit gateway in a secondary region, to ensure availability and fault tolerance.
{: note}

### High availability features
{: #high-availability-features}
  
{{site.data.keyword.dl_full_notm}} supports the following high availability features:

| Feature| Description | Consideration |
| -------------- | -------------- | -------------- |
| Multi-zone deployment | Deployed across multiple availability zones within a MZR | Deploy a transit gateway at the region level; for redundancy, consider deploying an additional transit gateway in a separate region. |
| GRE tunnel redundancy | Configure at least two GRE tunnels in different availability zones | Transit Gateway doesn't provide automatic GRE failover; manual configuration of multiple tunnels is required. |
| Global routing | Interconnect VPCs and classic infrastructure across different regions | Ensure proper configuration of routing policies and monitor inter-region traffic to maintain optimal performance. |
| Direct Link integration | Connect on-premises networks to IBM Cloud using Direct Link | Implement redundancy in on-premises connections to avoid single points of failure.                      |
| Multi-account support | Interconnect VPCs and classic infrastructure across multiple IBM Cloud accounts | Coordinate with account owners to manage permissions and ensure consistent configuration across accounts. |
{: caption="High availability features for {{site.data.keyword.tg_full_notm}}" caption-side="bottom"}

Customers are responsible for maintaining network connectivity into IBM Cloud. To ensure that you have a highly available, end-to-end connection, consider the following features:

| Feature| Description | Consideration |
| -------------- | -------------- | -------------- |
| Multiple devices on-premises | Set up multiple redundant devices (for example, routers and switches) on-premises| Plan for physical space, power, and cabling redundancy. Test failover scenarios regularly. |    |
| Connection to different AZs | Connect devices to different Availability Zones (AZs) within the same Multi-Zone Region (MZR) | Ensure diverse physical paths and coordinate with providers to avoid shared risk groups. |
| AS Prepending, BGP | Configure AS prepending and BGP routing to manage traffic flow between active and passive connections | Define clear routing policies for inbound and outbound traffic. Monitor BGP advertisements for correctness. |
{: caption="Customer HA features for {{site.data.keyword.tg_full_notm}}" caption-side="bottom"}
 
## Disaster recovery architecture
{: #disaster-recovery-intro}

IBM Cloud Transit Gateway supports disaster recovery by enabling secure, high-availability connectivity across IBM Cloud environments.

Deploying Transit Gateway across multiple AZs within a MZR ensures fault tolerance within a single region. This setup mitigates the impact of localized failures, maintaining connectivity between VPCs and classic infrastructure.

Using global routing capabilities allows for interconnecting VPCs and classic infrastructure across different regions. This approach supports workload distribution and failover between regions, enhancing the overall resilience of the network architecture.

By combining IBM Cloud Transit Gateway's features with strategic deployment and configuration practices, organizations can establish robust disaster recovery architectures that ensure continuity and minimize downtime during disruptions.

The following table outlines these features and key considerations.
 
### Disaster recovery features
{: #dr-features}

Transit Gateway supports the following disaster recovery features:
 
| Feature | Description | Consideration |
| -------------- | -------------- | -------------- |  
| Global routing | Supports interconnectivity between VPCs and classic infrastructure across different regions. | Facilitates workload distribution and failover between regions. |
{: caption="Disaster Recovery features for {{site.data.keyword.tg_full_notm}}" caption-side="bottom"}
 
As a customer, you can create and support the following other disaster recovery options:

| Feature | Description | Consideration |
| -------------- | -------------- | -------------- |  
| Global routing configuration | Configures global routing to interconnect VPCs and classic infrastructure across different regions. | Supports workload distribution and failover between regions. |                       |   |
| Direct Link integration | Integrates IBM Cloud Direct Link with Transit Gateway for dedicated, private connectivity between on-premises networks and IBM Cloud. | Requires proper configuration to avoid IP overlap and ensure seamless connectivity. |   
{: caption="Customer disaster recovery features for {{site.data.keyword.tg_full_notm}}" caption-side="bottom"}

### Planning for disaster recovery
{: #disaster-recovery-planning}

It’s critical to regularly practice your disaster recovery steps to ensure that you are well-prepared for unexpected disruptions. As you build your disaster recovery plan, consider the following failure scenarios and resolutions for IBM Cloud Transit Gateway.

There can be multiple ways to recover from certain failures, so be sure to assess each scenario based on your specific architecture and requirements. Here are common failure scenarios, along with potential recovery actions:

| Failure | Resolution |
| -------------- | -------------- |  
| Regional Transit Gateway outage   | Redirect traffic through a transit gateway in another region.                 |
| BGP session loss                  | Verify routing configuration and peer device status; restart the BGP session. |
| VPC attachment failure            | Recreate the attachment or fail over to an alternate path.                    |
| Accidental configuration deletion | Restore configuration using backups or automation tools.    |
| Logging or monitoring failure     | Reconfigure logging/monitoring endpoints; verify IAM and service status.      |
{: caption="Disaster recovery scenarios for {{site.data.keyword.tg_full_notm}}" caption-side="bottom"} 

### Backing up transit gateways for disaster recovery
{: #disaster-recovery-tgw}

Be prepared to re-create your transit gateways and connections. This section helps you ensure that you have all the data needed for this purpose.

{{site.data.keyword.tg_full_notm}} backups are cross-regionally durable. They are stored across multiple regions, and are restorable to other regions.
{: note}

The following steps use the IBM Cloud CLI, but you can also use the IBM Cloud console or API.
{: tip}

Preserve a list of all of your transit gateways and their connections. To do so, follow these steps:

1. Use the `ibmcloud tg gateways` command to list details about all your transit gateways. Save this output.
1. For each gateway, use the `ibmcloud tg connections GATEWAY_ID` command to list information about its connections. Save this output.

For more information, see the [Transit Gateway CLI reference](/docs/transit-gateway?topic=transit-gateway-transit-gateway-cli).
{: tip}

Saving the information that is returned from these commands helps you recover from a failure quickly. In the event of a failure, use the saved information and run the `ibmcloud tg gateway-create` and `ibmcloud tg connection-create` commands to re-create your transit gateways and connections.

## Your responsibilities for HA and DR
{: #ha-dr-responsibilities}

For background information about responsibility ownership for using Direct Link between {{site.data.keyword.IBM_notm}} and you, the customer, see [Understanding your responsibilities when using IBM Cloud Transit Gateway](/docs/transit-gateway?topic=transit-gateway-tg-responsibilities). It is your responsibility to continuously test your plan for HA and DR.

Interruptions in network connectivity and short periods of unavailability of a service might occur. It is your responsibility to make sure that application source code includes [client availability retry logic](/docs/resiliency?topic=resiliency-high-availability-design#client-retry-logic-for-ha) to maintain high availability of the application.   
{: note}  

## Recovery time objective (RTO) 
{: #rto-features}  

Transit Gateway provides mechanisms to protect your data and restore service functions. Business continuity plans are in place to achieve targeted [recovery time objective](#x3167918){: term} (RTO) for the service. The following table outlines the targets for Transit Gateway.

| Feature | RTO |
| -------------- | -------------- |
| Control plane availability        | < 1 hour       |
| Data path failover (intra-region) | < 5 minutes    |
| Data path failover (inter-region) | < 15 minutes   |
| Portal/API access                 | < 1 hour       |
| Configuration restoration         | < 4 hours      |
{: caption="RTO objectives for IBM Cloud Transit Gateway" caption-side="bottom"}

## Change management
{: #dl-change-management}

Change management includes tasks, such as configuration changes and deletion.

Grant users and processes the Identity and Access Management (IAM) roles and actions with the least privilege that is required for their work. For more information, see [How can I prevent accidental deletion of services?](/docs/resiliency?topic=resiliency-dr-faq#prevent-accidental-deletion).
{: tip} 

Best practices for managing change also include:
 
* Plan and document changes by maintaining a change log for any modifications that are made to your Transit Gateway configuration. 
* Create a backup of critical configurations before performing major changes.
* Schedule high-impact changes during low-traffic windows and notify impacted teams.
* Monitor your Transit Gateway health and metrics to ensure that everything is performing as expected. 

## How IBM supports disaster recovery planning
{: #ibm-disaster-recovery-planning}

Built for resiliency, IBM Cloud Transit Gateway simplifies and secures connectivity across VPCs, on-premises networks, and hybrid cloud environments. In the event of a failure:

* Incident response teams quickly identify and isolate the failure.
* Traffic rerouting is performed when possible using IBM’s backbone and provider networks.
* Service status communication is maintained through the IBM Cloud Status page to keep you informed.

When it comes to zone and regional failures, IBM takes the following recovery actions:

### How IBM recovers from zone failures
{: #ibm-zone-failure}

A zone failure refers to the failure of an availability zone within a region. In the event of a zone failure, IBM Cloud will identify the issue, perform repairs, and restore the zone as quickly as possible. If a zone becomes unavailable, traffic is automatically routed to healthy zones. Customers do not need to take any action to restore their transit gateway.

### How IBM recovers from regional failures
{: #ibm-regional-failure}

In the rare event of a regional failure, IBM Cloud will identify and repair the failure and restore the service to the region as quickly as possible. Transit gateway instances will be automatically restored as part of this process. After the region is back up, you are responsible for verifying the state of your transit gateway instances.

## How IBM maintains services
{: #ibm-service-maintenance}

All upgrades follow {{site.data.keyword.IBM_notm}} service best practices, including recovery plans and rollback processes. Regular maintenance might cause short interruptions, mitigated by [client availability retry logic](/docs/resiliency?topic=resiliency-high-availability-design#client-retry-logic-for-ha). Changes are rolled out sequentially, region by region, and zone by zone within a region. {{site.data.keyword.IBM_notm}} reverts updates at the first sign of a defect. 

IBM provides advance notice for all planned maintenance activities. If a change is expected to affect your workloads, IBM communicates this through official notifications. To stay updated on maintenance, service announcements, and other updates, see the [Monitoring notifications and status](/docs/account?topic=account-viewing-cloud-status) page.
