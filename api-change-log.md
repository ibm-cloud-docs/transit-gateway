---

copyright:
  years: 2022, 2023
lastupdated: "2023-06-24"

keywords: transit gateway api change log

subcollection: transit-gateway

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Transit Gateway API change log
{: #tg-api-changelog}

Check back regularly to see what's new with {{site.data.keyword.cloud}} Transit Gateway API.
{: shortdesc}

## 24 June 2023
{: #transit-gateway-jun2423}

{{site.data.keyword.powerSys_notm}} connections for transit gateways
:    Transit gateways now support {{site.data.keyword.powerSys_notm}} connections. A {{site.data.keyword.powerSys_notm}} connection allows {{site.data.keyword.powerSys_notm}} networks to connect to other networks (for instance, VPC and classic infrastructure) that are connected to the same transit gateway. This adds a new `network_type` value of `power_virtual_server` to the choices when creating a new connection. For details, see [Add connection to a Transit Gateway](/apidocs/transit-gateway#create-transit-gateway-connection).

   Currently, the Power Edge Router (PER) solution is available only in `DAL10`.
   {: note}

## 24 April 2023
{: #transit-gateway-apr2423}

Direct Link multi-account support
:    You can now create connections of type `directlink` for resources not owned by the gateway owner. For more information, see [Add connection to a Transit Gateway](/apidocs/transit-gateway#create-transit-gateway-connection).
