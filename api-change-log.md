---

copyright:
  years: 2020, 2025
lastupdated: "2025-11-06"

keywords: transit gateway api change log

subcollection: transit-gateway

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Transit Gateway API change log
{: #tg-api-changelog}

Check back regularly to see what's new with {{site.data.keyword.cloud}} Transit Gateway API.
{: shortdesc}

## 06 November 2025
{: #transit-gateway-nov0625}

VPN connections for transit gateways
:    Transit gateways now support VPN gateway connections. A VPN gateway connection allows VPN gateways to connect to other networks (for instance, VPC, Direct Link, classic infrastructure, and Power Virtual Server) that are connected to the same transit gateway. This adds a new `network_type` value of `vpn_gateway` to the choices when creating a new connection.

## 27 August 2025
{: #transit-gateway-aug2725}

GRE enhanced route propagation
:    Allows routes to propagate between all GRE tunnels connected to the same transit gateway. This enables data traffic to flow between GRE tunnels that were previously isolated. GRE tunnels connected to networks that couldn’t communicate before can now exchange traffic. For more information, see [GRE enhanced route propagation considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#gre-enhanced-route-propagation-considerations).

For information about the new `gre_enhanced_route_propagation` property, see [creating a transit gateway](/apidocs/transit-gateway#create-transit-gateway) and [updating a specific transit gateway](/apidocs/transit-gateway#update-transit-gateway).
        
The API also returns the following properties on a transit gateway:

* `gre_enhanced_route_propagation` - Indicates whether GRE enhanced route propagation is enabled or not.
* `connection_count` - The number of connections on the transit gateway.
* `connections_need_attention` - Indicates whether there are any connections on the transit gateway that require attention.

## 12 June 2024
{: #transit-gateway-jun1224}

Redundant Generic Routing Encapsulation (GRE)

:    To build in redundancy and eliminate the need to schedule an outage when a Transit Gateway router must go down for maintenance, there is a new **Redundant GRE**  connection type, which is essentially a grouping of at least two GRE tunnels that can connect to classic or VPC networks. This connection type allows GRE tunnels to be placed on different devices in the same zone and not flag overlapping routes that are in the redundant GRE's tunnels.

   Information for at least two GRE tunnels are required in the tunnel array on the `POST` call to create a redundant GRE. When retrieving connections, redundant GREs have a tunnel array listing the GRE tunnels within the redundant GRE. New APIs enable you to [create](/apidocs/transit-gateway?code=go#create-transit-gateway-gre-tunnel), [delete](/apidocs/transit-gateway?code=go#delete-transit-gateway-connection-tunnels), [update](/apidocs/transit-gateway?code=go#update-transit-gateway-connection-tunnels), and [retrieve](/apidocs/transit-gateway?code=go#get-transit-gateway-connection-tunnels) tunnels within a redundant GRE. This uses the tunnels resource on the REST API for a connection that is a redundant GRE.

   There is also a change to the `GET /locations/{name}` API, which now includes an array of zones that lists which zones are valid for GREs for a given region.

## 20 May 2024
{: #transit-gateway-may2024}

Transit Gateway connections list supports pagination
:    To improve performance and reliability, the operation to [retrieve all connections for a transit gateway](/apidocs/transit-gateway#list-transit-gateway-connections) has been enhanced to support pagination. With pagination, if you have more connections than the requested `limit` (default: 50, maximum 500) only the number of connections within the size limit are returned, sorted by date with the oldest first.

   While the default `limit` value allows your existing clients to retrieve the entire list of connections with one request, the default `limit` value is expected to be lowered in a future release. Additionally, we expect the number of transit gateway connections will continue to increase. Therefore, to ensure your clients continue to be aware of all connections, you must upgrade your clients to follow our [pagination guidance](/apidocs/transit-gateway#api-pagination). To test that your clients have been upgraded correctly, specify a `limit` value of `1`. For more information, see [Retrieves all connections](/apidocs/transit-gateway?code=go#list-connections).

   The SDK automatically handles pagination. No action is necessary.
   {: note} 

## 24 June 2023
{: #transit-gateway-ju2423}

{{site.data.keyword.powerSys_notm}} connections for transit gateways
:    Transit gateways now support {{site.data.keyword.powerSys_notm}} connections. A {{site.data.keyword.powerSys_notm}} connection allows {{site.data.keyword.powerSys_notm}} networks to connect to other networks (for instance, VPC and classic infrastructure) that are connected to the same transit gateway. This adds a new `network_type` value of `power_virtual_server` to the choices when creating a new connection. For details, see [Add connection to a Transit Gateway](/apidocs/transit-gateway#create-transit-gateway-connection).

## 24 April 2023
{: #transit-gateway-ap2423}

Direct Link multi-account support
:    You can now create connections of type `directlink` for resources not owned by the gateway owner. For more information, see [Add connection to a Transit Gateway](/apidocs/transit-gateway#create-transit-gateway-connection).
