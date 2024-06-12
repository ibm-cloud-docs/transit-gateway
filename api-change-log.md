---

copyright:
  years: 2022, 2024
lastupdated: "2024-06-12"

keywords: transit gateway api change log

subcollection: transit-gateway

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Transit Gateway API change log
{: #tg-api-changelog}

Check back regularly to see what's new with {{site.data.keyword.cloud}} Transit Gateway API.
{: shortdesc}

## 12 June 2024
{: #transit-gateway-june1224}

Redundant Generic Routing Encapsulation (GRE)

:    To build in redundancy and eliminate the need to schedule an outage when a Transit Gateway router must go down for maintenance, there is a new **Redundant GRE**  connection type, which is essentially a grouping of at least two GRE tunnels that can connect to classic or VPC networks. This connection type allows GRE tunnels to be placed on different devices in the same zone and not flag overlapping routes that are in the redundant GRE's tunnels.

   Information for at least two GRE tunnels are required in the tunnel array on the `POST` call to create a redundant GRE. When retrieving connections, redundant GREs have a tunnel array listing the GRE tunnels within the redundant GRE. New APIs enable you to [create](/apidocs/transit-gateway?code=go#create-transit-gateway-gre-tunnel), [delete](/apidocs/transit-gateway?code=go#delete-transit-gateway-connection-tunnels), [update](/apidocs/transit-gateway?code=go#update-transit-gateway-connection-tunnels), and [retrieve](/apidocs/transit-gateway?code=go#get-transit-gateway-connection-tunnels) tunnels within a redundant GRE. This uses the tunnels resource on the REST API for a connection that is a redundant GRE.

   There is also a change to the `GET /locations/{name}` API, which now includes an array of zones that lists which zones are valid for GREs for a given region.



## 24 June 2023
{: #transit-gateway-ju2423}

{{site.data.keyword.powerSys_notm}} connections for transit gateways
:    Transit gateways now support {{site.data.keyword.powerSys_notm}} connections. A {{site.data.keyword.powerSys_notm}} connection allows {{site.data.keyword.powerSys_notm}} networks to connect to other networks (for instance, VPC and classic infrastructure) that are connected to the same transit gateway. This adds a new `network_type` value of `power_virtual_server` to the choices when creating a new connection. For details, see [Add connection to a Transit Gateway](/apidocs/transit-gateway#create-transit-gateway-connection).

## 24 April 2023
{: #transit-gateway-ap2423}

Direct Link multi-account support
:    You can now create connections of type `directlink` for resources not owned by the gateway owner. For more information, see [Add connection to a Transit Gateway](/apidocs/transit-gateway#create-transit-gateway-connection).
