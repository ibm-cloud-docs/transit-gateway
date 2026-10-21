---

copyright:
  years: 2020, 2026
lastupdated: "2026-10-21"

keywords: use cases, interconnectivity, patterns, VPC, classic, GRE, Direct Link, VPN

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Interconnectivity patterns
{: #patterns}

{{site.data.keyword.tg_full_notm}} enables you to connect {{site.data.keyword.cloud_notm}} VPCs and classic infrastructure to transit gateways, allowing you to build global networks of multiple VPCs and classic infrastructure resources across {{site.data.keyword.cloud_notm}} regions to keep up with your business needs.
{: shortdesc}

{{site.data.keyword.tg_full_notm}} can connect to classic networks located in any MZR, regardless of the location of the transit gateway or the routing type specified.
{: note}

Here are some ways that you can implement the {{site.data.keyword.tg_full_notm}} service.

## Use case 1: Interconnect two or more VPCs in the same MZR
{: #use-case-1}

Connect two VPCs in the same region with a local transit gateway.

![Connect two or more VPCs in the same MZR](/images/TGW_SameRegion.png "Connect two or more VPCs in the same MZR"){: caption="Connect two or more VPCs in the same MZR" caption-side="bottom"}

## Use case 2: Interconnect two or more VPCs across multiple MZRs
{: #use-case-2}

Connect VPCs in multiple regions by using a global transit gateway.

![Connect two or more VPCs across multiple MZRs](/images/TGW_Multi-Multi.png "Connect two or more VPCs across multiple MZRs"){: caption="Connect two or more VPCs across multiple MZRs" caption-side="bottom"}

For higher resiliency, you can deploy multiple global transit gateways across regions and group them by using redundancy groups.
{: note}

## Use case 3: Interconnect one or more VPCs in the same MZR and an IBM classic network
{: #use-case-3}

Connect VPCs in the same region with {{site.data.keyword.cloud_notm}} classic through a local transit gateway.

![Connect to the IBM classic network and one or more VPCs in the same MZR](/images/TGW_Classic.png "Connect an IBM classic network and one or more VPCs in the same MZR"){: caption="Connect to the IBM classic network and one or more VPCs in the same MZR" caption-side="bottom"}

## Use case 4: Interconnect VPCs and an IBM classic network to access all your resources across all MZRs
{: #use-case-4}

Connect VPCs from multiple regions with {{site.data.keyword.cloud_notm}} classic through a global transit gateway.

![Connect to the IBM classic network and VPCs to access all your resources across all MZRs](/images/twg_use_4.png "Connect an IBM classic network and VPCs to access all your resources across all MZRs"){: caption="Connect to the IBM classic network and VPCs to access all your resources across all MZRs" caption-side="bottom"}

## Use case 5: Interconnect VPCs across accounts
{: #use-case-5}

Connect VPCs in the same region owned by different {{site.data.keyword.cloud_notm}} accounts through a local transit gateway.

![Connect two or more VPCs across accounts](/images/TGW_UC5_Cross_Account-VPC.png "Connect two or more VPCs across IBM Cloud accounts"){: caption="Connect two or more VPCs across accounts" caption-side="bottom"}

## Use case 6: Connect networks (VPC and classic) to multiple local gateways
{: #use-case-6}

Keep in mind:

- Your local traffic is kept on a local transit gateway, which reduces latency.
- Highly Available (HA) capabilities are provided, as data in VPCs C and D might be replicated in VPCs in E and F.
- Classic infrastructure transit gateway connections are required to be in the same account as the transit gateway owner.

![Connect networks (VPC and classic) to multiple gateways](/images/TGW_1.2.png "Connect networks (VPC and classic) to multiple gateways"){: caption="Connect networks (VPC and classic) to multiple local gateways" caption-side="bottom"}

## Use case 7: Interconnect networks (VPC and classic) across accounts
{: #use-case-7}

Connect cross-account {{site.data.keyword.cloud_notm}} classic accounts to one or more transit gateways. To do so, the {{site.data.keyword.cloud_notm}} account that owns the transit gateway requests permission from the {{site.data.keyword.cloud_notm}} classic account to connect it to the transit gateway. The {{site.data.keyword.cloud_notm}} classic account must approve the request before the connection is made. You can repeat this process for multiple {{site.data.keyword.cloud_notm}} classic account connections as shown.

![Connect both VPC and classic across accounts](/images/TGW_xac.png "Connect both VPCs and classic across IBM Cloud accounts"){: caption="Connect both VPC and classic across accounts" caption-side="bottom"}

## Use case 8: Connect networks by using a High Availability GRE tunnel
{: #use-case-8}

Connect {{site.data.keyword.cloud_notm}} classic infrastructure by using a GRE tunnel to a local transit gateway.

This diagram shows a highly available GRE tunnel configuration. When you set up a GRE tunnel configuration, an availability zone must be specified. To make this use case highly available, you must set up two GRE tunnels with the same endpoints, but by using different availability zones.

![Connect by using a GRE tunnel](/images/HA-GRE.png "Connect by using a High Availability GRE tunnel"){: caption="Connect networks using a High Availability GRE tunnel" caption-side="bottom"}

Transit gateway GRE connections require the gateway owner to specifically configure HA for their needs. A GRE connection is a point-to-point connection, has no built-in redundancy, and is a single point of failure. When you configure a GRE connection on a transit gateway, you must specify the availability zone. For a robust HA solution, configure multiple GRE connections by using different availability zones.
{: note}

## Use case 9: Connect an on-premises network by using Direct Link
{: #use-case-9}

Connect {{site.data.keyword.cloud_notm}} Direct Link to allow on-premises connectivity to {{site.data.keyword.cloud_notm}} networks through a transit gateway. This connection allows the on-premises network to access all networks that are connected to the transit gateway. In the following example, the Direct Link gateway connects to a global transit gateway, along with 4 VPCs and {{site.data.keyword.cloud_notm}} Classic Infrastructure. The inverse is also true, in that all other networks that are connected to the transit gateway are now connected to the on-premises network.

Direct Link can be connected to either local or remote transit gateways.
{: note}

![Connect On-Premise Network to Transit Gateway](/images/dlaas.png "Connect Direct Link on-premises network"){: caption="Connect on-premises network using Direct Link" caption-side="bottom"}

## Use case 10: Using VPN for VPC as a redundant spoke
{: #use-case-10}

In this use case, a VPN gateway is configured as a spoke to the transit gateway to provide a redundant network path between the on-premises environment and IBM Cloud. The primary connectivity is established using Direct Link, which offers private, dedicated connectivity with assured bandwidth and low-latency performance. This direct connection terminates in the IBM Cloud Transit VPC, which connects to the transit gateway. From there, traffic is routed to multiple environments including Power Virtual Servers, virtual server instances in spoke VPCs, and classic infrastructure.

To enhance availability without the added cost of a second direct link, a VPN gateway is deployed as a secondary path. This path provides secure connectivity over the internet, using BGP VPN tunnels between the on-prem network and the VPN gateway. Multiple GRE tunnels are established between the VPN gateway appliances and the transit gateway routers, allowing the VPN to act as a spoke within the Transit Gateway topology. While this path doesn't provide the same performance guarantees as Direct Link, it ensures continued connectivity during a primary path failure, making it a cost-effective and resilient solution for hybrid cloud networking.

![VPN gateway as a backup connection for Direct Link](/images/vpnaas.svg "VPN gateway as a backup connection for Direct Link"){: caption="VPN gateway as a backup connection for Direct Link" caption-side="bottom"}

## Use case 11: Build a highly available multi-region network
{: #build-ha-multi-region-network}

Deploy two global transit gateways in separate regions and group them into a redundancy group to create a resilient network architecture. In this example, Global Transit GW A is deployed in eu-es and Global Transit GW B is deployed in br-sao. Both gateways are members of the same redundancy group.

Two VPCs under Account A are connected to both transit gateways:

- **VPC A** (us-south, `10.4.0.0/16`) — connects locally to Transit GW A or B, and reaches VPC B (`10.5.0.0/16`) via Transit GW A or B
- **VPC B** (us-east, `10.5.0.0/16`) — connects locally to Transit GW A or B, and reaches VPC A (`10.4.0.0/16`) via Transit GW A or B

Because each VPC is connected to both transit gateways, traffic can be routed through either gateway. If one region becomes unavailable, the other gateway continues to forward traffic between the VPCs without interruption.

![Build a highly available multi-region network](/images/transit-gw-redundancy-group.svg "Build a highly available multi-region network"){: caption="Build a highly available multi-region network" caption-side="bottom"}





[Beta]{: tag-cyan}

## Use case 13: Single-zone dynamic route server with Transit Gateway
{: #use-case-12-drs}

In this use case, a VPC dynamic route server is connected to a transit gateway to enable automatic, BGP-based route distribution across connected networks. An Edge VPC acts as the network entry point, hosting a firewall and a dynamic route server appliance. The enterprise network connects to IBM Cloud over Direct Link, while a public address range provides internet-facing connectivity.

Within the Edge VPC, the firewall establishes an eBGP session with the dynamic route server. The dynamic route server connects to the transit gateway, which establishes GRE tunnels to the dynamic route server appliances and runs eBGP sessions over those tunnels. In this single-zone deployment, three dynamic route server appliances connect to two transit gateway devices, creating six GRE tunnels in a full mesh for redundancy.

The dynamic route server acts as a read-only spoke: it learns routes advertised by the transit gateway across its connections and distributes those routes to BGP peers within the VPC, including the firewall. This eliminates the need to manually maintain static routes as the network grows or changes. From the transit gateway, traffic is routed to connected environments, including classic infrastructure, Power Virtual Server workspaces, and spoke VPCs.

This use case is well suited for hybrid cloud environments that require dynamic, scalable route propagation across multiple networks without the overhead of managing static routes or separate VPN tunnels for each destination.

![Single-zone dynamic route server with Transit Gateway](/images/drs-vpn-export.svg "Dynamic route learning with a transit gateway"){: caption="[Single-zone dynamic route server with Transit Gateway" caption-side="bottom"}

## Use case 14: Multi-zone dynamic route server with Transit Gateway
{: #use-case-13-drs}

In this use case, dynamic route server appliances are deployed across multiple VPC zones and connected to a transit gateway to provide highly available, BGP-based route distribution between IBM Cloud and enterprise networks. An Edge VPC serves as the network entry point, hosting firewall and dynamic route server appliances that connect on premises networks, internet traffic, and cloud workloads through a centralized routing architecture.

The firewall establishes eBGP sessions with the dynamic route server appliances, while the transit gateway creates GRE tunnels and eBGP sessions with dynamic route server appliances in each zone. By distributing appliances across three zones and maintaining redundant connections to transit gateway devices, the design continues to exchange routing information even if a device, tunnel, or entire zone becomes unavailable.

The dynamic route server appliances learn routes from the transit gateway and advertise them to BGP peers within the VPC, including the firewall. This enables automatic route propagation between the enterprise network and IBM Cloud resources, including classic infrastructure, Power Virtual Server workspaces, and spoke VPCs, without requiring manual route updates as the environment evolves.

This use case is well suited for business-critical hybrid cloud deployments that require resilient, multi-zone connectivity and automated route distribution across a large and growing network footprint.

![Multi-zone dynamic route server with Transit Gateway](/images/multizone-drs.svg "Dynamic route learning with a transit gateway"){: caption="Multi-zone dynamic route server with Transit Gateway" caption-side="bottom"}



## Power Virtual Server use cases using Transit Gateway
{: #use-case-powervs}

For use cases involving {{site.data.keyword.powerSys_notm}} workspaces, see [Power Edge Router use cases](/docs/power-iaas?topic=power-iaas-network-architecture-diagrams#per-use-cases).
