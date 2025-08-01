---

copyright:
  years: 2020, 2025
lastupdated: "2025-07-22"

keywords: updates, additions, improvements

subcollection: transit-gateway

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for IBM Cloud Transit Gateway
{: #transit-gateway-release-notes}

Find out about new and updated features in {{site.data.keyword.tg_full}}.

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
