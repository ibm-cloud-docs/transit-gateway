---

copyright:
  years: 2020, 2021
lastupdated: "2021-04-01"

keywords: updates, additions, improvements

subcollection: transit-gateway

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank_"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:note: .note}
{:important: .important}

# Release notes for IBM Cloud Transit Gateway
{: #release-notes-for-ibm-cloud-load-balancer}

Find out about new and updated features in {{site.data.keyword.tg_full}}.

## March 2021
{: #march-2021}

### Classic infrastructure connections across IBM Cloud accounts
You can now connect to {{site.data.keyword.cloud}} classic infrastructure in another {{site.data.keyword.cloud_notm}} account by providing the cloud account ID when adding a connection to your transit gateway. The account containing the classic infrastructure is then able to view the gateway and all of its connections, and must choose to opt-in to allow account-to-account interconnectivity.

For more information, see [Adding a cross-account connection](/docs/transit-gateway?topic=transit-gateway-edit-gateway#adding-cross-account-connections).

## January 2021
{: #january-2021}

### Connect networks to multiple local gateways
You can now connect networks, VPCs, and classic connections to multiple local transit gateways. Previously, you could connect a network only to a single transit gateway. Now traffic between local networks can use a local gateway. In addition, if you need to connect to a remote network, you can attach to a global gateway. Routing of traffic between networks takes an optimized path (if multiple connections exist), meaning local traffic stays local to the region and is not charged.

The limit for the number of gateways per account has been updated to ten, and the limit of gateways per region to five. You can open an [IBM Support case](/docs/get-support?topic=get-support-using-avatar#using-avatar) if you need to expand your service limits further.

## July 2020
{: #july-2020}

### VPC connections across IBM Cloud accounts
You can now connect to a VPC in another IBM Cloud account by providing the CRN of the VPC when adding a connection to your transit gateway. The account containing the VPC is then able to view the gateway and all of its connections, and must choose to opt-in to allow account-to-account interconnectivity for that VPC.

For more information see [Adding a cross-account connection](/docs/transit-gateway?topic=transit-gateway-edit-gateway#adding-cross-account-connections)

### Open source SDKs
Open source Software Development Kits have now been published for use with Python, Node, Go, and Java platforms.
