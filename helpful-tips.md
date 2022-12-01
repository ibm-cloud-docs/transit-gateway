---

copyright:
  years: 2020, 2022
lastupdated: "2022-11-30"

keywords: help, tips, connections, provision

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Planning for IBM Cloud Transit Gateway
{: #helpful-tips}

Make sure that you review the following considerations before ordering your {{site.data.keyword.tg_full}}.
{: shortdesc}

## Service limits
{: #service-limits}

Keep in mind the following service limits while using IBM Cloud Transit Gateway.

| Service limit |  Default |
|---------------------------|------|
| Number of transit gateways | 10 gateways per account, 5 gateways per region |
| Number of connections per transit gateway |  * 10 IBM Cloud VPC connections  \n * 5 IBM Cloud classic connections  \n * 5 IBM Cloud Direct Link connections  \n * 5 {{site.data.keyword.powerSys_notm}} connections (IBM Internal Use Only) |
| Number of prefixes per connection | * 15 prefixes for VPC connections  \n * 120 prefixes for classic connections  \n * 120 prefixes for GRE connections  \n * 120 prefixes for Direct Link connections  \n * 120 prefixes for {{site.data.keyword.powerSys_notm}} connections (IBM Internal Use Only) |
| Number of connections with prefix filters | 2 connections with prefix filters per gateway|
| Number of prefix filters per connection | 10 prefix filters per connection|
| Number of GRE tunnels per transit gateway | 12 GRE tunnels per gateway|
| Number of unique base networks targeted by unbound GRE tunnels per transit gateway | 5 unique base networks targeted by unbound GRE tunnels per gateway|
{: caption="Table 1. IBM Cloud Transit Gateway service limits" caption-side="bottom"}

You can open an [IBM Support case](/docs/get-support?topic=get-support-using-avatar#using-avatar) if you need your service limits expanded.
{: note}

## General considerations
{: #general-considerations}

All prefixes of a VPC and all subnets of a classic network will connect to the transit gateway, so it's important that they do not overlap. When creating VPCs that are intended to connect to a transit gateway, make sure to create the VPCs with non-overlapping VPC prefixes.
{: important}

* {{site.data.keyword.tg_full_notm}} supports provisioning transit gateways in the regions listed in [IBM Cloud Transit Gateway locations](/docs/transit-gateway?topic=transit-gateway-tg-locations).
* Create your transit gateway in a location that makes sense for your workload. For example, if you are connecting two VPCs in the `us-south` (Dallas) region and one VPC in the `eu-de` (Frankfurt) region, creating your gateway in `us-south` region would be the most efficient for your workload.
* You cannot connect a [classic access VPC](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure) directly to a transit gateway. To connect the classic resources, use the {{site.data.keyword.cloud_notm}} classic infrastructure connection, and then all the resources in your classic access VPC are automatically connected.  
* You can connect a VPC, Direct Link or classic infrastructure to multiple local gateways and a single global gateway.
* Transit gateways and their connections can take several minutes after provisioning before they are available.
* Be descriptive when naming your transit gateway connections. When connecting to resources across accounts, you must specify a connection name. When connecting to resources in the same account as the transit gateway, the VPC name or the word 'classic' is the default selection and can be modified.
* {{site.data.keyword.tg_full_notm}} is a multi-tenant application, where a single instance of the software, and its supporting infrastructure, serves multiple customers. As a result, monitoring your bandwidth use is important. If you use too much bandwidth, your transit gateway instance may be suspended. If you suspect this is the case, check the transit gateway instance connection status to see if it is in a `Suspended` state. If so, [contact support](/docs/transit-gateway?topic=transit-gateway-getting-help-and-support) to reinstate it.

## Classic infrastructure connection considerations
{: #classic-infra-connection-considerations}

* To use a transit gateway to connect your VPCs to your IBM Cloud classic infrastructure, you must enable your classic account for virtual routing and forwarding (VRF) and link it to your IBM Cloud account. For information on enabling your account for VRF, see [Enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint).

* When you connect a VPC and the classic infrastructure to a transit gateway, all prefixes in the VPC become visible to the classic infrastructure VRF, which uses IP addresses in the `10.0.0.0/8` space. To ensure successful connectivity with the classic infrastructure, do not use prefixes in your VPCs that overlap with the `10.0.0.0/14`, `10.200.0.0/14`, `10.198.0.0/15`, and `10.254.0.0/16` blocks. Also, don't use addresses from your classic infrastructure subnets. To view a list of your classic infrastructure subnets, see [View all subnets](/docs/subnets?topic=subnets-view-all-subnets).

* Classic virtual server instances can have both a private (`eth0`) and a public (`eth1`) network interface. Currently, the routing tables for these interfaces point the default gateway to the public interface (`eth1`). You might have to add routing entries to route the subnets from other VPCs through the private interface.

* All of your IBM Cloud classic infrastructure networks across [MZRs](/docs/overview?topic=overview-locations#mzr-table) are accessible through this connection, regardless of the location of the transit gateway or the routing type specified.

* Classic infrastructure resources located in these [data centers](/docs/transit-gateway?topic=transit-gateway-tg-locations#szr-table) connect through a transit gateway to VPC resources.

* When classic infrastructure is connected to a transit gateway, it also includes any "Classic Access VPCs" attached to the account, because the subnets for these VPCs are associated with the classic infrastructure VRF. This is the only way to connect a transit gateway to a Classic Access VPC: by connecting the entire classic infrastructure to the transit gateway (instead of the specific Classic Access VPCs).

## Generic Routing Encapsulation (GRE) connection considerations
{: #gre-considerations}

When configuring a GRE tunnel, you must specify an availability zone in which to create the tunnel. Because of this, if for some reason that zone becomes unavailable, any network connected through a GRE tunnel on that zone is unreachable. To configure a highly available GRE tunnel, you must create a GRE tunnel in multiple zones, connecting the same endpoints.

GRE connections require the use of a BGP service between GRE tunnel IP addresses. The transit gateway configures a BGP service on the tunnel connection, before connecting to the other tunnel endpoint. Then, once the BGP protocol exchanges routes between the connected endpoint and the transit gateway, the GRE tunnel becomes the data path for the routed traffic.

GRE Tunnel routes are learned directly on BGP sessions established over the tunnel. For this reason, prefix filtering is not enabled for these connections.

The number of GRE tunnels connected to a transit gateway is quota limited. The default quota is 12.

Legacy GRE tunnel considerations:
   * Classic routes are not advertised through a traditional GRE tunnel.
   * Legacy GRE tunnels cannot communicate through other GRE tunnels on the same transit gateway.
   * Legacy GRE tunnels require a classic connection on the transit gateway before creation. As a result, all classic subnets will be advertised to all connections attached to the transit gateway, as well as any other of the connection's subnets on the classic network.

Unbound GRE tunnel Considerations:
   * Classic routes are advertised through an unbound GRE tunnel.
   * Unbound GRE tunnels can communicate through other unbound GRE tunnels connected to the same transit gateway in the same availability zone.
   * Unbound GRE tunnels cannot communicate with other unbound GRE tunnels on the same transit gateway if they are in a different availability zone. Unbound GRE tunnels in this scenario cannot be relied on for network isolation. 

   If you require network isolation, consider using separate transit gateways.
   {: tip}

   * Unbound GRE tunnels do not require a classic connection on the transit gateway. Classic network subnets will not be advertised to the connections on the transit gateway (or vice versa).
   * The default number of unique base networks that can be targeted by unbound GRE tunnel connections is limited to 5. You can open an [IBM Support case](/docs/get-support?topic=get-support-using-avatar#using-avatar) if you need these service limits expanded.

For more information and a use case example, refer to [Connect networks using a High Availability GRE tunnel](/docs/transit-gateway?topic=transit-gateway-about#use-case-8).

## Direct Link (2.0) connection consideration
{: #dl_considerations}

You can create Direct Link connections to a transit gateway to allow on-premises networks to connect to other networks in {{site.data.keyword.cloud_notm}}. After the direct link connects to the transit gateway, the on-premises network receives access to all other transit gateway connections. Likewise, all other networks connected to the transit gateway have access to the on-premises network. Direct Link connections follow the same process for physical or virtual cross connections as the standard Direct Link offering. After the connection is deleted from a transit gateway, the transit gateway operates as if it was never connected to a direct link.

The same network subnet considerations for transit gateway connections also apply to Direct Link connections. To ensure successful connectivity, do not use prefixes in your Direct Link connected network that overlap with other connections.
{: important}

## {{site.data.keyword.powerSys_notm}} connection consideration (IBM Internal Use Only)
{: #power_considerations}

You can connect a {{site.data.keyword.powerSys_notm}} instance to a transit gateway. This allows you to directly attach the {{site.data.keyword.powerSys_notm}} to a downstream transit gateway. After the {{site.data.keyword.powerSys_notm}} is connected to the transit gateway, your {{site.data.keyword.powerSys_notm}} service instance then has have access to all downstream transit gateway resources and services. Likewise, all downstream networks connected to the transit gateway will have access to the {{site.data.keyword.powerSys_notm}} instance. 

{{site.data.keyword.powerSys_notm}} connections can use Local or Global routing. However, only {{site.data.keyword.powerSys_notm}} instances in the same region as the transit gateway can use local routing. Also, a {{site.data.keyword.powerSys_notm}} instance can be connected to multiple transit gateways with local routing, but only one transit gateway with global routing. Downstream services will honor route preference based on the transit gateway type.

The same network subnet considerations for transit gateway connections also apply to {{site.data.keyword.powerSys_notm}} connections. To ensure successful connectivity, do not use prefixes in your {{site.data.keyword.powerSys_notm}} instance that overlap with other connections. Note that Transit Gateway provides prefix filtering to limit the prefixes being exposed, as well as a routing table report to see any overlaps after the connection is created.
{: important}

## VPC connection consideration
{: #vpc-connection-consideration}

{{site.data.keyword.cloud_notm}} VPC permits the use of RFC-1918 and IANA-registered IPv4 address space, privately within your VPC, with some exceptions in the IANA special-purpose ranges, and select ranges assigned to {{site.data.keyword.cloud_notm}} services. When using IANA-registered ranges within your enterprise, and within VPCs in conjunction with {{site.data.keyword.cloud_notm}} Transit Gateway, custom routes must be installed in each zone. For more information, see [Routing considerations for IANA-registered IP assignments](/docs/vpc?topic=vpc-interconnectivity#routing-considerations-iana).

## VPC interconnection consideration
{: #vpc-interconnection-consideration}

You can create a single transit gateway or multiple transit gateways to interconnect more than one IBM Cloud VPCs. You can also connect your IBM Cloud classic infrastructure to a transit gateway to provide seamless communication with classic infrastructure resources. For more information, refer to [Interconnecting VPCs](/docs/vpc?topic=vpc-interconnectivity&interface=cli#interconnecting-vpcs).

## Routing considerations
{: #routing-considerations}

* All connections to a transit gateway are connected to each other, so carefully consider all resources that you want to interconnect before deciding whether local or global routing is right for each gateway.

   Traffic from either routing option does not leave the private IBM Cloud network and is optimized for performance.
   {: note}

* If you plan to use your gateway to connect VPCs in the same multi-zone region ([MZR](/docs/overview?topic=overview-locations#mzr-table)), use local routing to provide connectivity to all accessible resources within the same MZR; for example, `us-south` (Dallas).

   ![Local routing](images/1-aboutLocalRoutingExample.png "Local routing"){: caption="Figure 1. Simple local routing example" caption-side="bottom"}

* If you plan to use your transit gateways to connect VPCs locally and between different [MZRs](/docs/overview?topic=overview-locations#mzr-table), use local gateways for VPCs in the same MZR, and a global gateway for VPCs across MZRs. You can use the example that follows a Highly Available (HA) scenario as well. All data in VPCs A and B can be replicated to VPCs C and D. If there is an issue in the US South region, connections reroute to US East.

   ![Global routing](images/2-aboutLocalAndGlobalRoutingExample.png "Local and Global routing"){: caption="Figure 2. Combining local and global routng example" caption-side="bottom"}

   Regardless of the routing type specified, {{site.data.keyword.tg_full_notm}} can connect to classic infrastructure networks located in any MZR. To achieve this, simply add the classic connection to your transit gateway.
   {: important}

* You can edit a gateway's routing type after it is provisioned. However, to change the routing type from global to local, you must first remove any global connections (that is, connections to resources that are not in the same location as the gateway). Note that connections to the IBM Cloud classic infrastructure are always considered local.

* When changing from Local to Global routing, you will be charged for all associated global connections. There is no impact to the network traffic when the routing type is changed.
