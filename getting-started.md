---

copyright:
  years: 2020, 2026
lastupdated: "2026-04-27"

keywords: transit, gateway, ordering, getting, started

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with IBM Cloud Transit Gateway
{: #getting-started}
{: help}
{: support}

Use {{site.data.keyword.tg_full}} to interconnect {{site.data.keyword.cloud_notm}} classic and Virtual Private Cloud (VPC) infrastructures worldwide, keeping traffic within the {{site.data.keyword.cloud_notm}} network. With {{site.data.keyword.tg_full_notm}}, organizations can define and control communication between resources on the {{site.data.keyword.cloud_notm}} network, providing dynamic scalability, high availability, and private, in-transit data between {{site.data.keyword.cloud_notm}} data centers. Transit gateways are commonly implemented to support hybrid workloads, frequent data transfers, private workloads, or to ease administration of the {{site.data.keyword.cloud_notm}} environment.
{: shortdesc}

With {{site.data.keyword.tg_full_notm}}, you can connect:

* VPCs within the same region (local routing)
* VPCs across different regions (global routing)
* VPCs to IBM Cloud classic infrastructure
* Power Virtual Server workspaces
* VPN gateways for site-to-site or client VPN connectivity
* On-premises networks using Direct Link connections
* External networks by using Generic Routing Encapsulation (GRE) tunnels
* Network resources across multiple IBM Cloud accounts (with appropriate access authorization)

To get started using {{site.data.keyword.tg_full_notm}}:

1. Review Transit Gateway features and use cases in [About {{site.data.keyword.tg_full_notm}}](/docs/transit-gateway?topic=transit-gateway-about).
1. Plan your topology and prerequisites. Identify the networks that you want to connect (VPC, classic, Power Virtual Server, VPN, Direct Link, or GRE) and ensure no overlapping CIDRs. For more information, see [Planning for {{site.data.keyword.tg_full_notm}}](/docs/transit-gateway?topic=transit-gateway-helpful-tips). 
1. Configure IAM permissions to allow users or service IDs to manage Transit Gateway resources. For more information, see [Using IAM permissions with IBM Cloud Transit Gateway](/docs/transit-gateway?topic=transit-gateway-iam).
1. Create a transit gateway in the target region. For more information, see [Ordering an {{site.data.keyword.tg_full_notm}}](/docs/transit-gateway?topic=transit-gateway-ordering-transit-gateway).
1. Add connections and configure routing. Attach networks, enable route propagation, and verify routes using route reports. Resolve routing conflicts (for example, overlapping CIDRs) using prefix filters. For more information, see [Adding a connection](/docs/transit-gateway?topic=transit-gateway-adding-connections) and [Generating a route report](/docs/transit-gateway?topic=transit-gateway-route-reports&interface=ui).
1. Configure Transit Gateway connection authorization to control which accounts or networks are allowed to attach and exchange traffic through the gateway. For more information, see [Using IAM permissions with IBM Cloud Transit Gateway](/docs/transit-gateway?topic=transit-gateway-iam).
1. Test traffic flow between networks and monitor behavior to confirm expected routing and access. For more information, see [Monitoring Transit Gateway](/docs/transit-gateway?topic=transit-gateway-monitoring). 
