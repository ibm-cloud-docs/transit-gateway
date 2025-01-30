---

copyright:
  years: 2020, 2025
lastupdated: "2025-01-30"

keywords: updates, additions, improvements

subcollection: transit-gateway

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for IBM Cloud Transit Gateway
{: #transit-gateway-release-notes}

Find out about new and updated features in {{site.data.keyword.tg_full}}. 

## 30 January 2025
{: #transit-gateway-jan3025}

Metrics routing support
:    You can now monitor and track metrics for Transit Gateway physical connections and virtual interfaces, allowing you to analyze traffic flow and set up alerts. This way, you can be notified and take appropriate action if any anomalies or unusual traffic patterns are detected. For more information, see [Monitoring Transit Gateway](/docs/transit-gateway?topic=transit-gateway-monitoring). 

## 12 June 2024
{: #transit-gateway-june1224}
{: release-note}

Support for redundant Generic Routing Encapsulation (GRE) tunnel connections
:   To build in redundancy and eliminate the need to schedule an outage when a Transit Gateway router must go down for maintenance, there is a new **Redundant GRE** connection type, which is essentially a grouping of at least two GRE tunnels that can connect to classic or VPC networks. This connection type allows GRE tunnels to be placed on different devices in the same zone and not flag overlapping routes that are in the redundant GRE's tunnels. For more information, see [Creating a redundant GRE tunnel](/docs/transit-gateway?topic=transit-gateway-redundant-gre-connection&interface=ui).

## 1 May 2024
{: #transit-gateway-may0124}
{: release-note}

Behavior change: Disable advertisement of service network routes from transit gateway connections
:   If any connection on a transit gateway advertises a service route, the service route is not advertised to any classic connections on that transit gateway. Before this change, Transit Gateway advertised all routes (from any connection) to all of its other connections. For more information, see [Preparing for Transit Gateway changes to advertised service network routes](/docs/transit-gateway?topic=transit-gateway-notification-dl-tgw).

## 24 June 2023
{: #transit-gateway-jun2423}
{: release-note}

{{site.data.keyword.powerSys_notm}} connections for transit gateways
:    Transit gateways now support {{site.data.keyword.powerSys_notm}} connections. A {{site.data.keyword.powerSys_notm}} connection allows a network to connect to other networks (for instance, VPC and classic infrastructure) that are connected to the same transit gateway. This adds a new Power Systems Virtual Server option when creating a new connection. For details, see [Adding a connection](/docs/transit-gateway?topic=transit-gateway-adding-connections&interface=ui).

## 22 June 2023
{: #transit-gateway-jun2223}
{: release-note}

Madrid multi-zone region (MZR) support
 :    Madrid MZR is now supported.

## 24 April 2023
{: #transit-gateway-apr2423}
{: release-note}

Multi-account support for IBM Cloud Direct Link
 :    Transit Gateway now includes cross-account support for Direct Link connections. For more information, see [Ordering a transit gateway](/docs/transit-gateway?topic=transit-gateway-ordering-transit-gateway) and [Adding a cross-account connection](/docs/transit-gateway?topic=transit-gateway-adding-cross-account-connections).

## 30 November 2022
{: #transit-gateway-jan2023}
{: release-note}

Unbound GRE tunnels
:    You can now use an unbound Generic Routing Encapsulation (GRE) tunnel transit gateway connection to connect endpoints, which allows a transit gateway to connect to overlay networks hosted on classic infrastructure resource. Unbound GRE tunnels have the following advantages over legacy GRE tunnels:
   * The ability to receive classic network subnets from a classic connection.
   * The ability to communicate through other unbound GRE tunnels on the same transit gateway.
   * Do not require a classic connection on the transit gateway. The classic network's subnets will not be advertised to all the connections on the transit gateway and vice versa.

:    See [Creating an unbound GRE tunnel](/docs/transit-gateway?topic=transit-gateway-unbound-gre-connection) for more information.


## 26 March 2022
{: #transit-gateway-mar2622}
{: release-note}

Network prefix filters
:    Simplify the management of the IP addresses that you reference in your resources to route network traffic. You can create prefix filters to permit or deny specific routes on specific connections. These prefix filters are added to an ordered list that is processed sequentially. A default filter (permit or deny all prefixes) is then applied after the prefix filter list is processed. For more information, see [Adding and deleting prefix filters](/docs/transit-gateway?topic=transit-gateway-adding-prefix-filters).

## 15 November 2021
{: #transit-gateway-nov1521}
{: release-note}

Transit Gateway route reports
:    You can now request a route report, which shows all routes known to a transit gateway and each of its connections. The report shows:
    * Border Gateway Protocol (BGP) information associated with these routes
    * Which connections supply which routes
    * Overlapping routes

:    For more information, see [Generating a transit gateway route report](/docs/transit-gateway?topic=transit-gateway-route-reports).

## 30 August 2021
{: #transit-gateway-aug3021}
{: release-note}

Direct Link connections for transit gateways
:    Transit gateways now support Direct Link connections. A Direct Link connection allows an on-premises network to connect to other networks (for instance, VPC and classic infrastructure) that are connected to the same transit gateway.

:    The beta release has ended. If you participated in this beta, you can continue to use the gateways that you created during the beta period.

## 17 June 2021
{: #transit-gateway-jun1721}
{: release-note}

Allow Generic Routing Encapsulation (GRE) connections for transit gateways
:    Transit gateways now support connections using GRE tunnels to connect endpoints. A GRE tunnel connection allows a transit gateway to connect to overlay networks hosted on classic infrastructure resources.

## 01 March 2021
{: #transit-gateway-mar0121}
{: release-note}

Classic infrastructure connections across IBM Cloud accounts
:    You can now connect to {{site.data.keyword.cloud}} classic infrastructure in another {{site.data.keyword.cloud_notm}} account by providing the cloud account ID when adding a connection to your transit gateway. The account containing the classic infrastructure is then able to view the gateway and all of its connections, and must choose to opt-in to allow account-to-account interconnectivity.

:    For more information, see [Adding a cross-account connection](/docs/transit-gateway?topic=transit-gateway-adding-cross-account-connections).

## 01 January 2021
{: #transit-gateway-jan0121}
{: release-note}

Connect networks to multiple local gateways
:    You can now connect networks, VPCs, and classic connections to multiple local transit gateways. Previously, you could connect a network only to a single transit gateway. Now traffic between local networks can use a local gateway. In addition, if you need to connect to a remote network, you can attach to a global gateway. Routing of traffic between networks takes an optimized path (if multiple connections exist), meaning local traffic stays local to the region and is not charged.

:    The limit for the number of gateways per account has been updated to ten, and the limit of gateways per region to five. You can open an [IBM Support case](/docs/account?topic=account-using-avatar#using-avatar) if you need to expand your service limits further.

## 01 July 2020
{: #transit-gateway-jul-0120}

VPC connections across IBM Cloud accounts
:    You can now connect to a VPC in another IBM Cloud account by providing the CRN of the VPC when adding a connection to your transit gateway. The account containing the VPC is then able to view the gateway and all of its connections, and must choose to opt-in to allow account-to-account interconnectivity for that VPC.

:    For more information, see [Adding a cross-account connection](/docs/transit-gateway?topic=transit-gateway-adding-cross-account-connections&interface=ui).

Open source SDKs
:    Open source Software Development Kits have now been published for use with Python, Node, Go, and Java platforms.
