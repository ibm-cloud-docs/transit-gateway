---

copyright:
  years: 2020, 2025
lastupdated: "2025-12-08"

keywords: faq, faqs, questions

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# FAQ for IBM Cloud Transit Gateway
{: #faqs-for-transit-gateway}

These frequently asked questions can help you when working with the {{site.data.keyword.tg_full}}.
{: shortdesc}

## What are the differences between IBM Cloud Transit Gateway and IBM Cloud Direct Link?
{: #differences}
{: faq}
{: support}

[IBM Cloud Direct Link](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl) provides connectivity from an external source into a customer's {{site.data.keyword.cloud_notm}} private network. {{site.data.keyword.tg_full_notm}} provides connectivity between resources within a customer's {{site.data.keyword.cloud_notm}} private network.

## Where can I find Transit Gateway pricing?
{: #transit-gateway-pricing}
{: faq}
{: support}

You can estimate the cost of a transit gateway using the cost estimator on the provisioning page for {{site.data.keyword.tg_full_notm}}. For example, from the [{{site.data.keyword.cloud_notm}} console](/login){: external}, click the Navigation Menu icon ![Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**. Click **Create** to open the provisioning page.

For more information, see [Pricing considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#pricing-considerations).
{: note}

## What is changing in billing for GRE traffic?
{: #transit-gateway-gre-billing}
{: faq}
{: support}

Starting 12 January 2026, IBM Cloud Transit Gateway will begin billing for data transferred toward GRE tunnels. Previously, only traffic flowing from GRE tunnels toward other connections was billed, while traffic toward GRE tunnels was not. This update aligns GRE connections with the existing usage-based billing model applied to other connection types such as VPC, Direct Link, and Power Virtual Server. 

This means:
- If data flows into a GRE tunnel, charges will now apply.
- Traffic from GRE tunnels toward other connections was already billed and remains unchanged.
- GRE traffic will be billed at the same rate as other Transit Gateway connection types.

The following table shows the change in billing behavior:

| Source\Destination | uGRE/rGRE | GRE tunnel | Classic | VPC | PowerVS | Direct Link |
|------------------|-----------|------------|---|---|---|---|
| **uGRE/rGRE**   | 0x → 1x  | 0x → 1x | 1x | 1x  | 1x | 1x |
| **GRE tunnel**  | 0x → 1x  | 0x → 1x | 1x | 1x  | 1x | 1x |
| **Classic**     | 0x → 1x  | 0x → 1x | 1x | 1x  | 1x | 1x |
| **VPC**         | 0x → 1x  | 0x → 1x | 1x | 1x  | 1x | 1x |
| **PowerVS**     | 0x → 1x  | 0x → 1x | 1x | 1x  | 1x | 1x |
| **Direct Link** | 0x → 1x  | 0x → 1x | 1x | 1x  | 1x | 1x |

**Legend:**  
- **0x → 1x** = Previously not billed, now billed  
- **1x** = Already billed, remains unchanged 

## If I connect a classic connection to a transit gateway provisioned with local routing, does that mean I can only communicate with classic infrastructure resources that are in the same location as the transit gateway?
{: #communicate-same-resources}
{: faq}
{: support}

A classic connection allows you to communicate with all of your global classic infrastructure resources across MZRs, even if it is connected to a transit gateway provisioned with local routing.

The routing option that you choose for a transit gateway only determines what VPCs you can connect to it. Local routing restricts you to connecting VPCs in the same MZR as the transit gateway, while global routing allows you to connect any VPC across the MZRs. Select the routing option that is right for your applications - pricing is changed accordingly.

## Can I create more than one transit gateway in my account?
{: #gateway_create}
{: faq}
{: support}

You can create more than one transit gateway in your account. Each transit gateway (and its connections) are logically isolated from your other transit gateways.

## Can I create more than two connections for a given transit gateway?
{: #connections-faq}
{: faq}
{: support}

You can connect multiple VPCs in the same region to a single transit gateway with the local routing option, and connect them across regions by using global routing. Keep in mind that all of a transit gateway's network connections are interconnected, so carefully consider all resources that you want to connect. Make sure each connection receives a unique name in the gateway, and that you choose the appropriate routing type (local or global) based on the location of the connections.

## Can I connect to a VPC or classic infrastructure in another {{site.data.keyword.cloud_notm}} account?
{: #connect-vpc-in-another-account}
{: faq}
{: support}

You can connect to both a VPC or classic infrastructure in another {{site.data.keyword.cloud_notm}} account by providing the appropriate connection information when adding a connection to your transit gateway. The account containing the VPC or classic infrastructure is then able to view the gateway and all of its connections, and must choose to opt-in to allow account-to-account interconnectivity for that VPC. For more information, see [Adding a cross-account connection](/docs/transit-gateway?topic=transit-gateway-adding-cross-account-connections).

## How many connection requests can I make from one account to VPCs in other {{site.data.keyword.cloud_notm}} accounts?
{: #connection-requests-account-vpcs}
{: faq}
{: support}

Each gateway is only permitted to have ten outstanding requests for a cross-account connection.

## I connected a VPC to one transit gateway. Can I connect that VPC to a second transit gateway?
{: #connections-two-vpcs}
{: faq}
{: support}

You can connect a VPC to multiple local transit gateways and a single global gateway.

## I connected a classic connection to one transit gateway. Can I connect the classic connection to a second transit gateway?
{: #connections-two-tg}
{: faq}
{: support}

You can connect a classic connection to multiple local transit gateways and a single global transit gateway.

## Can I connect a direct link to both a VPC and a transit gateway simultaneously?
{: #connections-local-tgws}
{: faq}
{: support}

No, you must choose to connect to a direct resource (VPC or classic infrastructure), or bind your direct link to one or more local transit gateways, or one global gateway. Your on-premises network can then access IBM Cloud resources connected through the transit gateways.

## I can only provision a transit gateway in a certain set of locations on the provisioning page. Does that mean that the VPC I want to connect must be located in one of those locations?
{: #connections-locations}
{: faq}
{: support}

By enabling global routing, you can connect VPCs located in different [MZRs](/docs/overview?topic=overview-locations#table-mzr), regardless of the set of locations that you can provision your transit gateway in.

## What are the service limits that I must keep in mind while using {{site.data.keyword.tg_full_notm}}?
{: #service-limits-faq}
{: faq}
{: support}

For more information, see [Service limits](/docs/transit-gateway?topic=transit-gateway-helpful-tips#service-limits).

## Classic access VPCs can't be attached to a transit gateway. How can I connect and access classic resources in those VPCs?
{: #classic-resources}
{: faq}
{: support}

Although [classic-access VPCs](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure) can't be attached to a transit gateway, access to classic resources and classic-access VPC resources can be achieved by adding the classic infrastructure connection to a transit gateway. For more information, see [Classic infrastructure connection considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#classic-infra-connection-considerations).

## How can "VPC peering" be achieved on {{site.data.keyword.cloud_notm}}?
{: #vpc-peering}
{: faq}
{: support}

{{site.data.keyword.tg_full_notm}} can be used to connect multiple VPCs to each other. As such, connecting/peering two VPCs is just a part of the functionality that the transit gateway service offers. {{site.data.keyword.cloud_notm}} does not provide a standalone VPC peering service or capability.

## Can I connect a VPN or a direct link to a transit gateway?
{: #vpn}
{: faq}
{: support}

{{site.data.keyword.cloud_notm}} Direct Link can be connected to either a local or global transit gateway.

Currently, you can't connect a VPN to a transit gateway.

## Can I create a global transit network using the {{site.data.keyword.tg_full_notm}}?
{: #global-transit}
{: faq}
{: support}

{{site.data.keyword.tg_full_notm}} enables standard IP routing between networks (for example, global VPCs) that are connected to it. You can add additional functionality by configuring {{site.data.keyword.IBM_notm}} or third-party virtual network functions, such as VPN, NAT, and firewalls, within one or more of the interconnected networks (for instance, using the "Transit VPC" concept).

## How can I guarantee one of my clients is not going to impact the others? 
{: faq}
{: #client-impact}

Capacity management handles the overall available capacity on the transit gateway and is subject to our weekly capacity management review. When the device reaches roughly a 50% load, we augment the connectivity to the device. 
 
## What scalability options do I have for my transit gateway? Does it manage itself? How do I know if it's reaching maximum capacity?
{: faq}
{: #scalability}

The {{site.data.keyword.cloud_notm}} infrastructure manages all transit gateways. There are no scalability options available.

## How do you prevent Distributed Denial of Service (DDoS) attacks? What restrictions do you have in place? 
{: faq}
{: #ddos}

Neither third-parties nor the internet can see your transit gateway traffic. As no critical information, such as IP router addresses, is open to anyone but you, DDoS attacks can't bring down the network. In addition, a typical Multi-protocol Label Switching service (MPLS) uses packet filtering and applies access control lists (ACLs) to limit access. Only the ports with routing protocols from a specific area of the network can access the information.

## How does my transit gateway handle encryption for connectivity between VPCs?
{: faq}
{: #vpc-encryption}

{{site.data.keyword.tg_full_notm}} does not perform encryption; it only provides connectivity. Encryption between VPCs is your own responsibility.

It is an RFC-2547-based platform where the core network and network address are 100% concealed. 

## What are the tools for monitoring the consumption of resources associated with the service, as well as the costs and the quality of the service?
{: faq}
{: #account}

{{site.data.keyword.tg_full_notm}} is integrated into the [IBM Cloud usage dashboard](/docs/account?topic=account-viewingusage), which provides a summary of estimated charges for all services and resources that are used per month in your organizations. This includes the number of connections and the amount of traffic flowing across your transit gateways. {{site.data.keyword.tg_full_notm}} usage is billed and reported as part of the [IBM Cloud invoice process](/docs/account?topic=account-managing-invoices).

## Are there notifications through email for events of unavailability of the service?
{: faq}
{: #service-unavailability-notifications}

You should use the standard [IBM Cloud notification process](/docs/account?topic=account-viewing-notifications) for any maintenance events.

## Can I generate a route report for a transit gateway?
{: faq}
{: #faq-route-reports}

Yes, you can. For detailed instructions, see [IBM Cloud Transit Gateway route reports](/docs/transit-gateway?topic=transit-gateway-route-reports).

## Can I interconnect VPCs using a transit gateway?
{: faq}
{: #faq-interconnecting-vpcs}

You can create a single transit gateway or multiple transit gateways to interconnect more than one IBM Cloud VPCs. You can also connect your IBM Cloud classic infrastructure to a transit gateway to provide seamless communication with classic infrastructure resources. For more information, refer to [Interconnecting VPCs](/docs/vpc?topic=vpc-interconnectivity&interface=cli#interconnecting-vpcs).

## In a Highly Available (HA) configuration, how long after the failover of the primary GRE tunnel does the routing device wait before declaring it inactive?
{: faq}
{: #faq-stale-routes-time}

This time, by default, is set as 5 minutes (300 seconds), and defined by the configuration statement `stale-routes-time`. The `stale-routes-time` statement allows you to set the length of time the routing device waits to receive messages from restarting neighbors before declaring them inactive. This means, in the case of a GRE HA failover to a second GRE tunnel, the traffic takes 5 minutes to be reflected by the second tunnel. 

## My existing transit gateway doesn't support ECMP. What can I do?
{: faq}
{: #faq-ecmp}

If your transit gateway doesn’t support ECMP (Equal-Cost Multi-Path Routing) and you need it for improved traffic routing, you can [open a support case](/docs/account?topic=account-open-case&interface=ui). IBM Support can assist in enabling ECMP for your transit gateway, allowing your traffic to be distributed across multiple paths for better redundancy and load balancing.

## Can I use multiple local BGP ASNs within the same zone?
{: faq}
{: #faq-multiple-local-bgp-asns}

 No. IBM Cloud Transit Gateway assigns a single local ASN per zone because each zone is backed by a specific data center. This means all connections within the same zone will share the same local ASN by design.

If you require different local ASNs for isolation purposes (for example, per tenant), the only workaround is to create connections in different zones. Currently, the platform doesn't support assigning multiple local ASNs within a single zone.
