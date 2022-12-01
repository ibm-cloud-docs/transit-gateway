---

copyright:
  years:  2020, 2022
lastupdated: "2022-11-30"

keywords: change log for transit gateway, updates to transit gateway

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Transit gateway CLI change log
{: #cli-change-log}

In this change log, you can learn about the latest changes, improvements, and updates for {{site.data.keyword.tg_full}}.

## 30 November 2022
{: #cli-november3022}

Unbound GRE tunnels
:    You can now use an unbound Generic Routing Encapsulation (GRE) tunnel connection to connect endpoints, which allows a transit gateway to connect to overlay networks hosted on classic infrastructure resource.
:    New commands:

    * `base-network-type` - Network type of the base connection (classic). For use only with the `unbound_gre_tunnel` network type.
    * `network-account-id` - ID of account to connect to a classic connection. For use only with the `classic` type when the account of the connection is different than the gateway's account.
    * `network-type` - Network type of the GRE connection. Values are `gre_tunnel` or `unbound_gre_tunnel`. The default value is `gre_tunnel`.

For more information, see [ibmcloud tg connection-create-gre](/docs/tg-cli-plugin?topic=tg-cli-plugin-transit-gateway-cli#connection-create-gre).

## 26 March 2022
{: #cli-mar2622}

Network prefix filters
:    Simplify the management of the IP addresses that you reference in your resources to route network traffic. You can create prefix filters to permit or deny specific routes on specific connections. These prefix filters are added to an ordered list that is processed sequentially. A default filter (permit or deny all prefixes) is then applied after the prefix filter list is processed. For more information, see [Adding and deleting prefix filters](/docs/transit-gateway?topic=transit-gateway-adding-prefix-filters&interface=cli). 

## 15 November 2021
{: #cli-nov1521}

Transit gateway route reports
:    You can now request a route report, which shows all routes known to a transit gateway and each of its connections. The report shows:

    * Border Gateway Protocol (BGP) information associated with these routes
    * Which connections supply which routes
    * Overlapping routes

:    For more information, see [Generating a transit gateway route report](/docs/transit-gateway?topic=transit-gateway-route-reports&interface=cli).

## 30 August 2021
{: #cli-aug3021}

Direct Link (2.0) connections for transit gateways
:    Transit gateways now support Direct Link (2.0) connections. A Direct Link connection allows an on-premises network to connect to other networks (for instance, VPC and classic infrastructure) that are connected to the same transit gateway.

## 17 June 2021
{: #cli-jun1721}

Allow Generic Routing Encapsulation (GRE) connections for transit gateways
:    Transit gateways now support connections using GRE tunnels to connect endpoints. A GRE tunnel connection allows a transit gateway to connect to overlay networks hosted on classic infrastructure resources.

## 01 March 2021
{: #cli-mar0121}

Classic infrastructure connections across IBM Cloud accounts
:    You can now connect to {{site.data.keyword.cloud}} classic infrastructure in another {{site.data.keyword.cloud_notm}} account by providing the cloud account ID when adding a connection to your transit gateway. The account containing the classic infrastructure is then able to view the gateway and all of its connections, and must choose to opt-in to allow account-to-account interconnectivity.

:    For more information, see [Adding a cross-account connection](/docs/transit-gateway?topic=transit-gateway-edit-gateway#adding-cross-account-connections&interface=cli).

## 01 January 2021
{: #cli-jan0121}

Connect networks to multiple local gateways
:    You can now connect networks, VPCs, and classic connections to multiple local transit gateways. Previously, you could connect a network only to a single transit gateway. Now traffic between local networks can use a local gateway. In addition, if you need to connect to a remote network, you can attach to a global gateway. Routing of traffic between networks takes an optimized path (if multiple connections exist), meaning local traffic stays local to the region and is not charged.

:    The limit for the number of gateways per account has been updated to ten, and the limit of gateways per region to five. You can open an [IBM Support case](/docs/get-support?topic=get-support-using-avatar#using-avatar) if you need to expand your service limits further.

## 01 July 2020
{: #cli-jul-0120}

VPC connections across IBM Cloud accounts
:    You can now connect to a VPC in another IBM Cloud account by providing the CRN of the VPC when adding a connection to your transit gateway. The account containing the VPC is then able to view the gateway and all of its connections, and must choose to opt-in to allow account-to-account interconnectivity for that VPC.

:    For more information, see [Adding a cross-account connection](/docs/transit-gateway?topic=transit-gateway-edit-gateway#adding-cross-account-connections&interface=cli).
