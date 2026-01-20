---

copyright:
  years: 2020, 2026
lastupdated: "2026-01-20"

keywords: updates, additions, improvements

subcollection: transit-gateway

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for IBM Cloud Transit Gateway
{: #transit-gateway-release-notes}

Find out about new and updated features in {{site.data.keyword.tg_full}}.

## 21 January 2026
{: #transit-gateway-jan2026}

Prefix filtering for GRE connections
:   You can now set up prefix filters on GRE connections to control which routes are accepted from GRE peers. For cross-account GRE connections, the transit gateway owner manages the filters, since GRE peers already control which routes they advertise. By default, a filter that allows all routes is automatically applied to all GRE connections. Existing connections will continue accepting all routes unless you create custom prefix filters.

## 06 November 2025
{: #transit-gateway-nov0625}

Support for VPN gateway connections
:    You can now create VPN gateway connections to a transit gateway in {{site.data.keyword.cloud_notm}} using route-based VPNs over redundant GRE tunnels. Attaching a VPN gateway to a transit gateway requires a dynamic VPN connection. This connection type enables more efficient and scalable hybrid cloud networking, allowing services like Power Virtual Server to seamlessly connect through VPN gateway connections. For more information, see [VPN gateway connection considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#vpn-connection-considerations).

## 27 August 2025
{: #transit-gateway-au0825}

GRE enhanced route propagation
:    Allows routes to propagate between all GRE tunnels connected to the same transit gateway. This enables data traffic to flow between GRE tunnels that were previously isolated. GRE tunnels connected to networks that couldn’t communicate before can now exchange traffic.

:    This option reduces the need to create multiple GRE tunnels for communication between route tables in the same multi-zone region. By default, the **GRE enhanced route propagation** toggle is disabled to maintain existing behavior. For more information, see [GRE enhanced route propagation considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#gre-enhanced-route-propagation-considerations).

## 27 March 2025
{: #transit-gateway-mar2725}

4-way ECMP support now available
:    Newly created transit gateways now support 4-way ECMP. Existing gateways can be [enabled upon request](/docs/transit-gateway?topic=transit-gateway-faqs-for-transit-gateway&interface=ui#faq-ecmp). For more information, see [ECMP planning considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#ecmp-considerations).

## 13 March 2025
{: #transit-gateway-mar1325}

Montreal region now available
:    Montreal is now a supported region for the Transit Gateway service, available in zone `ca-mon-1` for Generic Routing Encapsulation (GRE) tunnels. For more information, see [IBM Cloud region and data center locations for resource deployment](/docs/overview?topic=overview-locations).

## 30 January 2025
{: #transit-gateway-jan3025}

Metrics routing support
:    You can now monitor and track metrics for Transit Gateway physical connections and virtual interfaces, allowing you to analyze traffic flow and set up alerts. This way, you can be notified and take appropriate action if any anomalies or unusual traffic patterns are detected. For more information, see [Monitoring Transit Gateway](/docs/transit-gateway?topic=transit-gateway-monitoring).

## 12 June 2024
{: #transit-gateway-june1224}
{: release-note}

Support for redundant GRE tunnel connections
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

:    For more information, see [Creating an unbound GRE tunnel](/docs/transit-gateway?topic=transit-gateway-unbound-gre-connection).
