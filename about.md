---

copyright:
  years: 2020, 2026
lastupdated: "2026-09-15"

keywords: features, overview

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# About {{site.data.keyword.tg_full_notm}}
{: #about}

As the number of your Virtual Private Clouds (VPCs) grows, you need a way to manage the interconnection between these resources across multiple regions. {{site.data.keyword.tg_full}} is designed specifically for this purpose.
{: shortdesc}

With {{site.data.keyword.tg_full_notm}}, you can create single or multiple transit gateways to connect VPCs together. You can also connect your {{site.data.keyword.cloud_notm}} classic infrastructure to a transit gateway to provide seamless communication with classic infrastructure resources. Any new network that you connect to a transit gateway is then automatically made available to every other network connected to it so that you can scale your network as it grows.

Transit gateways provide flexibility by allowing you to add networks to local gateways. Networks can be attached to multiple local gateways and a single global gateway, enabling you to keep local traffic on a local gateway.

## Overview of features
{: #feature-overview}

{{site.data.keyword.tg_full_notm}} offers the following features:

### Privacy
{: #privacy}

* Connections to and from an {{site.data.keyword.tg_full_notm}} on the IBM private network are not exposed to the public internet, thus reducing public egress and VPN costs and reducing security threats.

* {{site.data.keyword.tg_full_notm}} is a fully redundant, fault-tolerant service with no single point of failure within these [{{site.data.keyword.cloud_notm}} Multi-Zone Regions (MZR)](/docs/transit-gateway?topic=transit-gateway-tg-locations).

### Security and access management
{: #security-iam}

{{site.data.keyword.tg_full_notm}} integrates with Identity and Access Management (IAM), letting you manage access to your transit gateway. Using IAM, you can create and manage [{{site.data.keyword.cloud_notm}} users and groups](/docs/transit-gateway?topic=transit-gateway-iam), as well as user permissions to allow or deny their access.

### Routing
{: #routing}

{{site.data.keyword.tg_full_notm}} supports local and global routing between VPCs and the {{site.data.keyword.cloud_notm}} classic infrastructure. All routing options remain within the private {{site.data.keyword.cloud_notm}} infrastructure without operating on the public internet, and are optimized for performance. {{site.data.keyword.tg_full_notm}} allows customers greater flexibility, redundancy, and speed in scaling their workloads, and in connecting isolated networks that run on {{site.data.keyword.cloud_notm}}.

For global routing deployments, you can optionally configure redundancy groups to enable multiple transit gateways in different regions to share routing behavior. This configuration improves resiliency by allowing traffic to continue flowing if a region becomes unavailable and helping to optimize routing paths between networks.

### Redundancy groups for high availability
{: #redundancy-groups-for-ha}

Redundancy groups enable you to deploy multiple global transit gateways across regions that operate together as a single logical routing domain.

When transit gateways are part of the same redundancy group:

- They share routing behavior across regions.
- Connected networks can communicate through multiple gateways.
- Traffic can continue to flow even if a region becomes unavailable.
- Routing might favor gateways that are closer to the source network.

This configuration extends global routing by providing additional resiliency and flexibility for multi-region network designs.

A redundancy group is defined during transit gateway creation by assigning a shared group name. Transit gateways with the same group name automatically participate in the same redundancy group.

To achieve redundancy, you must configure the same network connections on each transit gateway in the group.
{: important}

### Prefix filtering
{: #prefix-filtering}

{{site.data.keyword.tg_full_notm}} supports prefix filtering on connections, allowing you to control which routes are advertised to and from each connected network. You can permit or deny specific prefixes to prevent unintended route propagation and reduce the risk of routing conflicts. For more information, see [Adding and deleting prefix filters](/docs/transit-gateway?topic=transit-gateway-adding-prefix-filters).

### Route reports
{: #route-reports}

{{site.data.keyword.tg_full_notm}} provides route reports that display all the routes known to a transit gateway across its connections. Route reports help you verify connectivity, identify overlapping prefixes, and troubleshoot routing issues before they affect traffic. For more information, see [Generating a route report](/docs/transit-gateway?topic=transit-gateway-route-reports&interface=ui).

### Optimized traffic and fault tolerance
{: #vpc-optimized-traffic-fault-tolerance}

Transit Gateway is a regional service that employs routers located in each Availability Zone. In a typical setup, when virtual server instances are deployed across different VPCs, these instances attempt to communicate with each other. Traffic between VPCs remains within the same zone, ensuring efficient local routing and optimized data transfer.

This standard behavior also applies when using a transit VPC and advertising static routes from one VPC to advertise the same prefix across all zones. Even if firewalls are deployed within the VPCs (resulting in duplicate firewalls in the other advertised zones), traffic still favors the transit gateway in its respective zone. This routing behavior ensures that traffic returns through the same zone's transit gateway, maintaining routing within the same zone. VPCs typically prioritize the transit gateway within their zone, minimizing cross-zone traffic.

During a zonal failure, such as when a transit gateway experiences a failure in one zone (resulting from the failure of all zone's routers), communication could be disrupted. In such cases, traffic might be routed differently, with one direction of traffic sent through an alternate path, while the response might return from a different route. In general, though, VPC traffic typically remains within the same zone.
{: note}

For multi-region deployments, redundancy groups extend this fault tolerance by enabling traffic to fail over to transit gateways in other regions.

### Easily connect across boundaries
{: #boundaries}

{{site.data.keyword.tg_full_notm}} interconnects your {{site.data.keyword.cloud_notm}} VPCs with compute and classic resources across the globe. You can also interconnect VPCs and classic resources across {{site.data.keyword.cloud_notm}} accounts.

IBM Cloud Transit Gateway supports the use of Generic Routing Encapsulation (GRE) tunnels to connect endpoints. GRE tunnels enable the transit gateway to connect to overlay networks hosted on classic infrastructure resources for unique use cases.

With GRE enhanced route propagation enabled, all GRE tunnels connected to the same transit gateway share routes and can communicate across zones. When this setting is disabled, network traffic cannot be exchanged between unbound GRE tunnels in different zones or between tunnels within redundant GREs. For more information, see [GRE tunnels](/docs/transit-gateway?topic=transit-gateway-gre-connection&interface=ui).

### Direct Link connectivity
{: #directlink}

{{site.data.keyword.tg_full_notm}} supports Direct Link connections. Connecting Direct Link to your {{site.data.keyword.tg_full_notm}} on-premises network grants access to all networks connected on the transit gateway. Similarly, all other connections on the transit gateway have access to your network. As with other network connections to the {{site.data.keyword.tg_full_notm}}, special consideration must be taken to avoid IP overlap issues. For more information, see [Dealing with overlapping VPC prefixes and classic infrastructure subnets](/docs/transit-gateway?topic=transit-gateway-overlapping-vpc-prefixes-and-classic-subnets).

### VPN gateway connectivity
{: #vpn-connectivity}

{{site.data.keyword.tg_full_notm}} supports VPN gateway connections, enabling on-premises or external networks to connect with other networks in {{site.data.keyword.cloud_notm}} over secure IPsec tunnels. The VPN gateway acts as a spoke within the transit gateway architecture, using dynamic routing with eBGP over redundant GRE tunnels to provide scalable and resilient connectivity. For more information, see [VPN gateway connection considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#vpn-connection-considerations).





### {{site.data.keyword.powerSys_notm}} connectivity
{: #powervs}

{{site.data.keyword.tg_full_notm}} supports {{site.data.keyword.powerSys_notm}} connections. Connecting a {{site.data.keyword.powerSys_notm}} instance to your {{site.data.keyword.tg_full_notm}} network grants access to all networks connected on the transit gateway. Similarly, all other connections on the transit gateway have access to your network. As with other network connections to the {{site.data.keyword.tg_full_notm}}, special consideration must be taken to avoid IP overlap issues. For more information, see [Dealing with overlapping VPC prefixes and classic infrastructure subnets](/docs/transit-gateway?topic=transit-gateway-overlapping-vpc-prefixes-and-classic-subnets).

## Interconnectivity patterns
{: #patterns}

For examples of how you can implement {{site.data.keyword.tg_full_notm}} to interconnect VPCs, classic infrastructure, Direct Link, VPN gateways, and Power Virtual Server resources across accounts and regions, see [Interconnectivity patterns](/docs/transit-gateway?topic=transit-gateway-patterns).
