---

copyright:
  years: 2020, 2025
lastupdated: "2025-08-27"

keywords: help, tips, connections, provision

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Planning for IBM Cloud Transit Gateway
{: #helpful-tips}

Make sure that you review the following considerations before ordering your {{site.data.keyword.tg_full}}.
{: shortdesc}

## General considerations
{: #general-considerations}

All prefixes of a VPC and all subnets of a classic network will connect to the transit gateway, so it's important that they don't overlap. When creating VPCs that are intended to connect to a transit gateway, make sure to create the VPCs with non-overlapping VPC prefixes.
{: important}

* {{site.data.keyword.tg_full_notm}} supports provisioning transit gateways in the regions listed in [IBM Cloud Transit Gateway locations](/docs/transit-gateway?topic=transit-gateway-tg-locations).
* Create your transit gateway in a location that makes sense for your workload. For example, if you are connecting two VPCs in the `us-south` (Dallas) region and one VPC in the `eu-de` (Frankfurt) region, creating your gateway in `us-south` region would be the most efficient for your workload.
* You can't connect a [classic access VPC](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure) directly to a transit gateway. To connect the classic resources, use the {{site.data.keyword.cloud_notm}} classic infrastructure connection, and then all the resources in your classic access VPC are automatically connected.
*  A transit gateway requires at least two connections before network traffic can flow over the transit gateway. Transit gateways that have less than two connections for 45 days or more are subject to be reclaimed (suspended, then deleted after 30 days).
* You can connect a VPC, Direct Link, or classic infrastructure to multiple local gateways and a single global gateway.
* Transit gateways and their connections can take several minutes after provisioning before they are available.
* Be descriptive when naming your transit gateway connections. When connecting to resources across accounts, you must specify a connection name. When connecting to resources in the same account as the transit gateway, the VPC name or the word 'classic' is the default selection and can be modified.
* {{site.data.keyword.tg_full_notm}} is a multi-tenant application, where a single instance of the software, and its supporting infrastructure, serves multiple customers. As a result, monitoring your bandwidth use is important. If you use too much bandwidth, your transit gateway instance may be suspended. If you suspect this is the case, check the transit gateway instance connection status to see if it is in a `Suspended` state. If so, [contact support](/docs/transit-gateway?topic=transit-gateway-getting-help-and-support) to reinstate it.
* The following ASNs are blocked on Transit Gateway Generic Routing Encapsulation (GRE) and Direct Link connections. Avoid using these ASNs on appliances so that they are not included on the advertised routes in the AS path. Having these ASNs included prevent networks from working properly.

    `0`, `13884`, `36351`, `64512`, `64513`, `65100`, `65200-65234`, `65402-65433`, `65500`, `65516`, `65519`, `65521`, `65531` and `4201065000-4201065999`

## ECMP considerations
{: #ecmp-considerations} 

   * When planning for ECMP (Equal-Cost Multi-Path), keep in mind that throughput won't scale linearly with the number of direct links. For example, if you connect two 10 GB direct links to an ECMP-capable transit gateway, you won’t get 20 GB throughput; you'll see more than 10 GB, but less than 20 GB. This is because ECMP works on a per-stream or per-source basis, meaning if traffic comes from a single endpoint, it will likely favor one link, not both. To achieve more balanced throughput, it's recommended to drive traffic from multiple sources, as this will distribute the load more evenly across the available direct links.
   * Limitation: ECMP doesn't work for direct links on a single router. Instead, it is supported across multiple routers with direct links, as long as those routers are advertising the same prefix.
   * Known restriction: New transit gateways support 4-way ECMP, but existing gateways can't use this feature unless you [open a support case](/docs/account?topic=account-open-case&interface=ui) for assistance. 

      If you don't want the ECMP feature enabled on your transit gateways, you can open a support case to be added to a denylist, which will disable this feature on your gateways.
      {: note}

## Pricing considerations
{: #pricing-considerations}

The [IBM Cloud cost estimator](https://cloud.ibm.com/estimator), located on the Transit Gateway provisioning page, can't interpret network connection types. To get a reliable cost estimate, input the estimated number of transit gateways and connections. Keep in mind that if you create a redundant GRE, each tunnel is an individual connection that counts against your [connection limit](/docs/transit-gateway?topic=transit-gateway-helpful-tips#service-limits).

## Classic infrastructure connection considerations
{: #classic-infra-connection-considerations}

* To use a transit gateway to connect your VPCs to your IBM Cloud classic infrastructure, you must enable your classic account for virtual routing and forwarding (VRF) and link it to your IBM Cloud account. For information on enabling your account for VRF, see [Enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint).

* When you connect a VPC and the classic infrastructure to a transit gateway, all prefixes in the VPC become visible to the classic infrastructure VRF, which uses IP addresses in the `10.0.0.0/8` space. To ensure successful connectivity with the classic infrastructure, don't use prefixes in your VPCs that overlap with the `10.0.0.0/14`, `10.200.0.0/14`, `10.198.0.0/15`, and `10.254.0.0/16` blocks. Also, don't use addresses from your classic infrastructure subnets. To view a list of your classic infrastructure subnets, see [View all subnets](/docs/subnets?topic=subnets-view-all-subnets).

* Classic virtual server instances can have both a private (`eth0`) and a public (`eth1`) network interface. Currently, the routing tables for these interfaces point the default gateway to the public interface (`eth1`). You might have to add routing entries to route the subnets from other VPCs through the private interface.

* All of your IBM Cloud classic infrastructure networks across [MZRs](/docs/overview?topic=overview-locations#table-mzr) are accessible through this connection, regardless of the location of the transit gateway or the routing type specified.

* Classic infrastructure resources located in these [data centers](/docs/transit-gateway?topic=transit-gateway-tg-locations#szr-table) connect through a transit gateway to VPC resources.

* When classic infrastructure is connected to a transit gateway, it also includes any "Classic Access VPCs" attached to the account, because the subnets for these VPCs are associated with the classic infrastructure VRF. This is the only way to connect a transit gateway to a Classic Access VPC: by connecting the entire classic infrastructure to the transit gateway (instead of the specific Classic Access VPCs).

* Classic connections residing in the same data center are unable to communicate with each other if they are in a different region than the transit gateway.

## Generic Routing Encapsulation (GRE) connection considerations
{: #gre-considerations}

Review the following considerations for your particular GRE connection.

### General GRE connection considerations
{: #gre-general-considerations}

* When configuring a GRE tunnel, you must specify an availability zone in which to create the tunnel. Because of this, if for some reason that zone becomes unavailable, any network connected through a GRE tunnel on that zone is unreachable. To configure a highly available GRE tunnel, you must create a GRE tunnel in multiple zones, connecting the same endpoints.
* GRE connections require the use of a BGP service between GRE tunnel IP addresses. The transit gateway configures a BGP service on the tunnel connection, before connecting to the other tunnel endpoint. Then, once the BGP protocol exchanges routes between the connected endpoint and the transit gateway, the GRE tunnel becomes the data path for the routed traffic.
* GRE tunnel routes are learned directly on BGP sessions established over the tunnel. For this reason, prefix filtering is not enabled for these connections.
* The number of GRE tunnels connected to a transit gateway is quota limited. The default quota is 12.
* If you are using equal-cost paths between GRE and Direct Link (the same path length), the Direct Link is preferred instead of load balancing between the GRE and Direct Link.

### Redundant GRE considerations
{: #redundant-gre-connection-considerations}

* A redundant GRE is essentially a grouping of at least two GRE tunnels.
* The number of tunnels can't exceed two tunnels per zone.
* You can place the tunnels within a redundant GRE in the same or different zones.
* All connections and tunnels on the transit gateway must have unique names.
* All tunnels in a redundant GRE target the same network and account.
* When using the `VPC` base network type:
   * You must enable the IP spoofing flag for VPC network type. For information about enabling IP spoofing checks, see [About IP spoofing](/docs/vpc?topic=vpc-ip-spoofing-about).
   * The virtual server interface profile must be v2.
   * The local gateway IP:
      *  Must comply with [RFC 1918](/docs/transit-gateway?topic=transit-gateway-helpful-tips#vpc-connection-consideration) (or there are no floating IPs or public gateways on the VPC).
      * Must not be an IP address within the multicast range of `224.0.0.0` to `239.255.255.255` and can't be in conflict with any existing networks that are connected to the transit gateway.
      * Can't be used as the `local-gateway-ip` for another GRE using the same underlay network. 

* GRE enhanced route propagation:

   * When disabled (default), all tunnels within a redundant GRE don’t have their routes propagated to each other and can’t communicate with each other. However, redundant GRE tunnels can have their routes propagated to GRE tunnels outside the redundant GRE that are connected to the same transit gateway and are in the same zone.

   * When enabled, all GRE tunnels propagate their routes to other GREs if they’re connected to the same transit gateway.

### Unbound GRE tunnel considerations
{: #unbound-gre-connection-considerations}

* Classic routes are advertised through an unbound GRE tunnel.
* Can communicate through other unbound GRE tunnels connected to the same transit gateway in the same availability zone.
* Unbound GRE tunnels on the same transit gateway, located in different availability zones, can't communicate unless GRE enhanced route propagation is enabled. However, having GRE enhanced route propagation disabled shouldn't be relied on for network isolation as the absence of unbound GRE cross-zone traffic doesn't guarantee enforced separation.

If you require network isolation, consider using separate transit gateways.
{: tip}

* Do not require a classic connection on the transit gateway. Classic network subnets won't be advertised to the connections on the transit gateway (or vice versa).
* The default number of unique base networks that can be targeted by unbound GRE tunnels is limited to five. You can open an [IBM Support case](/docs/account?topic=account-using-avatar#using-avatar) if you need these service limits expanded.

For more information and a use case example, see [Connect networks using a High Availability GRE tunnel](/docs/transit-gateway?topic=transit-gateway-about#use-case-8).

### Legacy GRE considerations
{: #legacy-gre-connection-considerations}

* Classic routes are not advertised through a traditional GRE tunnel.
* Can't communicate through other GRE tunnels on the same transit gateway.
* Require a classic connection on the transit gateway before creation. As a result, all classic subnets will be advertised to all connections attached to the transit gateway, as well as any other of the connection's subnets on the classic network.

## Direct Link connection consideration
{: #dl_considerations}

You can create Direct Link connections to a transit gateway to allow on-premises networks to connect to other networks in {{site.data.keyword.cloud_notm}}. After the direct link connects to the transit gateway, the on-premises network receives access to all other transit gateway connections. Likewise, all other networks connected to the transit gateway have access to the on-premises network. Direct Link connections follow the same process for physical or virtual cross connections as the standard Direct Link offering. After the connection is deleted from a transit gateway, the transit gateway operates as if it was never connected to a direct link.

The same network subnet considerations for transit gateway connections also apply to Direct Link connections. To ensure successful connectivity, don't use prefixes in your Direct Link connected network that overlap with other connections.
{: important}

## {{site.data.keyword.powerSys_notm}} connection considerations
{: #power-considerations}

You can connect a {{site.data.keyword.powerSys_notm}} instance to a transit gateway. This allows you to directly attach the {{site.data.keyword.powerSys_notm}} to a downstream transit gateway. After the {{site.data.keyword.powerSys_notm}} is connected to the transit gateway, your {{site.data.keyword.powerSys_notm}} service instance then has have access to all downstream transit gateway resources and services. Likewise, all downstream networks connected to the transit gateway will have access to the {{site.data.keyword.powerSys_notm}} instance.

{{site.data.keyword.powerSys_notm}} connections can use Local or Global routing. However, only {{site.data.keyword.powerSys_notm}} instances in the same region as the transit gateway can use local routing. Also, a {{site.data.keyword.powerSys_notm}} instance can be connected to multiple transit gateways with local routing, but only one transit gateway with global routing. Downstream services will honor route preference based on the transit gateway type.

The same network subnet considerations for transit gateway connections also apply to {{site.data.keyword.powerSys_notm}} connections. To ensure successful connectivity, don't use prefixes in your {{site.data.keyword.powerSys_notm}} instance that overlap with other connections. Note that Transit Gateway provides prefix filtering to limit the prefixes being exposed, as well as a routing table report to see any overlaps after the connection is created.
{: important}



## VPC considerations
{: #vpc-connection-consideration}

* {{site.data.keyword.cloud_notm}} VPC permits the use of [RFC-1918](https://datatracker.ietf.org/doc/html/rfc1918){: external} and IANA-registered IPv4 address space, privately within your VPC, with some exceptions in the IANA special-purpose ranges, and select ranges assigned to {{site.data.keyword.cloud_notm}} services. When using IANA-registered ranges within your enterprise, and within VPCs in conjunction with {{site.data.keyword.cloud_notm}} Transit Gateway, custom routes must be installed in each zone. For more information, see [Routing considerations for IANA-registered IP assignments](/docs/vpc?topic=vpc-interconnectivity#routing-considerations-iana).

* You can create a single transit gateway or multiple transit gateways to interconnect more than one IBM Cloud VPCs. You can also connect your IBM Cloud classic infrastructure to a transit gateway to provide seamless communication with classic infrastructure resources. For more information, refer to [Interconnecting VPCs](/docs/vpc?topic=vpc-interconnectivity&interface=cli#interconnecting-vpcs).

* Bare Metal in VPC is not supported.

## Routing considerations
{: #routing-considerations}

* All connections to a transit gateway are connected to each other, so carefully consider all resources that you want to interconnect before deciding whether local or global routing is right for each gateway.

   Traffic from either routing option does not leave the private IBM Cloud network and is optimized for performance.
   {: note}

* If you plan to use your gateway to connect VPCs in the same multi-zone region ([MZR](/docs/overview?topic=overview-locations#table-mzr)), use local routing to provide connectivity to all accessible resources within the same MZR; for example, `us-south` (Dallas).

   ![Local routing](/images/1-aboutLocalRoutingExample.png "Local routing"){: caption="Simple local routing example" caption-side="bottom"}

* If you plan to use your transit gateways to connect VPCs locally and between different [MZRs](/docs/overview?topic=overview-locations#table-mzr), use local gateways for VPCs in the same MZR, and a global gateway for VPCs across MZRs. You can use the example that follows a Highly Available (HA) scenario as well. All data in VPCs A and B can be replicated to VPCs C and D. If there is an issue in the US South region, connections reroute to US East.

   ![Global routing](/images/2-aboutLocalAndGlobalRoutingExample.png "Local and Global routing"){: caption="Combining local and global routing example" caption-side="bottom"}

   Regardless of the routing type specified, {{site.data.keyword.tg_full_notm}} can connect to classic infrastructure networks located in any MZR. To achieve this, simply add the classic connection to your transit gateway.
   {: important}

* You can edit a gateway's routing type after it is provisioned. However, to change the routing type from **Global** to **Local**, you must first remove any global connections (that is, connections to resources that are not in the same location as the gateway). Note that connections to the IBM Cloud classic infrastructure are always considered Local.

* When changing from **Local** to **Global** routing, you will be charged for all associated global connections. There is no impact to the network traffic when the routing type is changed.

{{site.data.content.reuse-route-report-considerations}}

## Service limits
{: #service-limits}

Keep in mind the following service limits while using IBM Cloud Transit Gateway.

| Service limit |  Default |
|---------------------------|------|
| Number of transit gateways | 10 gateways per account, 5 gateways per region |
| Number of connections per transit gateway |  * 10 IBM Cloud VPC connections  \n * 5 IBM Cloud classic connections  \n * 5 IBM Cloud Direct Link connections  \n * 5 {{site.data.keyword.powerSys_notm}} connections |
| Number of prefixes per connection | * 25 prefixes for VPC connections  \n * 120 prefixes for classic connections  \n * 120 prefixes for GRE connections  \n * 120 prefixes for Direct Link connections  \n * 120 prefixes for {{site.data.keyword.powerSys_notm}} connections |
| Number of connections with prefix filters | 2 connections with prefix filters per gateway|
| Number of prefix filters per connection | 10 prefix filters per connection|
| Number of GRE tunnels per transit gateway | 12 GRE tunnels per gateway|
| Number of unique base networks targeted by unbound GRE tunnels per transit gateway | 5 unique base networks targeted by unbound GRE tunnels per gateway|
{: caption="IBM Cloud Transit Gateway service limits" caption-side="bottom"}

You can open an [IBM Support case](/docs/account?topic=account-using-avatar#using-avatar) if you need your service limits expanded.
{: note}
