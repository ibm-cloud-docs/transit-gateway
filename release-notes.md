---

copyright:
  years: 2020, 2021
lastupdated: "2021-11-15"

keywords: updates, additions, improvements

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for IBM Cloud Transit Gateway
{: #transit-gateway-release-notes}

Find out about new and updated features in {{site.data.keyword.tg_full}}.

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

Direct Link (2.0) connections for transit gateways
:    Transit gateways now support Direct Link (2.0) connections. A Direct Link connection allows an on-premises network to connect to other networks (for instance, VPC and classic infrastructure) that are connected to the same transit gateway.

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

:    For more information, see [Adding a cross-account connection](/docs/transit-gateway?topic=transit-gateway-edit-gateway#adding-cross-account-connections).

## 01 January 2021
{: #transit-gateway-jan0121}
{: release-note}

Connect networks to multiple local gateways
:    You can now connect networks, VPCs, and classic connections to multiple local transit gateways. Previously, you could connect a network only to a single transit gateway. Now traffic between local networks can use a local gateway. In addition, if you need to connect to a remote network, you can attach to a global gateway. Routing of traffic between networks takes an optimized path (if multiple connections exist), meaning local traffic stays local to the region and is not charged.

:    The limit for the number of gateways per account has been updated to ten, and the limit of gateways per region to five. You can open an [IBM Support case](/docs/get-support?topic=get-support-using-avatar#using-avatar) if you need to expand your service limits further.

## 01 July 2020
{: #transit-gateway-jul-0120}

VPC connections across IBM Cloud accounts
:    You can now connect to a VPC in another IBM Cloud account by providing the CRN of the VPC when adding a connection to your transit gateway. The account containing the VPC is then able to view the gateway and all of its connections, and must choose to opt-in to allow account-to-account interconnectivity for that VPC.

:    For more information, see [Adding a cross-account connection](/docs/transit-gateway?topic=transit-gateway-edit-gateway#adding-cross-account-connections).

Open source SDKs
:    Open source Software Development Kits have now been published for use with Python, Node, Go, and Java platforms.
