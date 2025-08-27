---

copyright:
  years:  2020, 2025
lastupdated: "2025-08-27"

keywords: change log for transit gateway, updates to transit gateway

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Transit Gateway CLI change log
{: #cli-change-log}

In this change log, you can learn about the latest changes, improvements, and updates for {{site.data.keyword.tg_full}}.

## 27 August 2025
{: #cli-august2725}

GRE enhanced route propagation
:    Allows routes to propagate between all GRE tunnels connected to the same transit gateway. This enables data traffic to flow between GRE tunnels that were previously isolated. GRE tunnels connected to networks that couldn’t communicate before can now exchange traffic.

   New command options:

    * [**`tg gateway-create`**](/docs/transit-gateway?topic=transit-gateway-transit-gateway-cli&interface=ui#gateway-create) and [**`tg gateway-update`**](/docs/transit-gateway?topic=transit-gateway-transit-gateway-cli&interface=ui#gateway-update) - Added a new boolean option `gre_enhanced_route_propagation` to enable or disable this feature. If not specified, the option is `false`. 

## 12 June 2024
{: #cli-june1224}

Redundant GRE tunnel connections support
:    To build in redundancy and eliminate the need to schedule an outage when a Transit Gateway router must down for maintenance, there is a new redundant GRE type, which is essentially a grouping of at least two GRE tunnels that can connect to classic or VPC networks. This connection type allows GRE tunnels to be placed on different devices in the same zone and not flag overlapping routes that are in the redundant GRE's tunnels. For more information, see [Creating a redundant GRE tunnel](/docs/transit-gateway?topic=transit-gateway-redundant-gre-connection&interface=ui).

   New commands:

    * [**`tg connection-rgre-create`**](/docs/transit-gateway?topic=transit-gateway-transit-gateway-cli#connection-create-redundant-gre) - Create a redundant GRE.
    * [**`tg redundant-gre-tunnel-add`**](/docs/transit-gateway?topic=transit-gateway-transit-gateway-cli#redundant-gre-tunnel-add) - Add a tunnel to a redundant GRE.
    * [**`tg redundant-gre-tunnel-remove`**](/docs/transit-gateway?topic=transit-gateway-transit-gateway-cli#redundant-gre-tunnel-remove) - Remove a tunnel from a redundant GRE.

## 20 May 2024
{: #cli-may2024}

Pagination support
:    To improve performance and reliability, the [**`ibmcloud tg connections`**](/docs/transit-gateway?topic=transit-gateway-transit-gateway-cli#list-connections) command has been enhanced to support pagination. With pagination, if you have more connections than the requested `limit` (default: 100, maximum 500) only the number of connections within the size limit are returned, sorted by date with the oldest first.

   To avoid disruption, upgrade your CLI version and update your tooling that uses CLI to handle the pagination. To test that your tooling handles pagination correctly, set the `limit` size on the [**`ibmcloud tg connections`**](/docs/transit-gateway?topic=transit-gateway-transit-gateway-cli#list-connections) command. For more information, see [Preparing for connection lists pagination support](/docs/transit-gateway?topic=transit-gateway-notification-tgw-pagination-support-connections-lists).

## 24 June 2023
{: #cli-june2424}

{{site.data.keyword.powerSys_notm}} connections for transit gateways
:    Transit gateways now support {{site.data.keyword.powerSys_notm}} connections. A {{site.data.keyword.powerSys_notm}} connection allows {{site.data.keyword.powerSys_notm}} networks to connect to other networks (for instance, VPC and classic infrastructure) that are connected to the same transit gateway. For details, see [**`ibmcloud tg connection-create`**](/docs/transit-gateway?topic=transit-gateway-transit-gateway-cli#connection-create).

## 24 April 2023
{: #cli-apr-2423}

Direct Link multi-account support
:    Changed command: You can now create a connection of type `directlink` to pass into the [**`connection-create`**](/docs/transit-gateway?topic=transit-gateway-transit-gateway-cli&interface=ui#connection-create) command and create a direct link from a different account owner. Previously only connections of type `vpc` and `classic` were allowed.

## 30 November 2022
{: #cli-november3022}

Unbound GRE tunnels
:    You can use an unbound Generic Routing Encapsulation (GRE) tunnel connection to connect endpoints, which allows a transit gateway to connect to overlay networks hosted on classic infrastructure resource.

   New [**`tg connection-create-gre`**](/docs/transit-gateway?topic=transit-gateway-transit-gateway-cli&interface=cli#connection-create-gre) command options:

    * `base-network-type` - Network type of the base connection (classic). For use only with the `unbound_gre_tunnel` network type.
    * `network-account-id` - ID of account to connect to a classic connection. For use only with the `classic` type when the account of the connection is different than the gateway's account.
    * `network-type` - Network type of the GRE connection. Values are `gre_tunnel` or `unbound_gre_tunnel`. The default value is `gre_tunnel`.
