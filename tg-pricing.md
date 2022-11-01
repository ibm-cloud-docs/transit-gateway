---

copyright:
  years: 2020
lastupdated: "2020-04-16"

keywords: about, features, overview

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Pricing examples for IBM Cloud Transit Gateway
{: #tg-pricing}

A new pricing structure now exists for transit gateways, changing the rates in regards to the number of connections, as well as to the amount of data transferred. For specific information on the new pricing structure, refer to [IBM Cloud Transit Gateway pricing](https://www.ibm.com/cloud/transit-gateway/pricing).
{: important}

The following examples describe various pricing scenarios for {{site.data.keyword.tg_full_notm}}.

When connecting to resources across accounts, the owner of the transit gateway is responsible for all connection and data transfer fees.
{: note}

## Example 1: Locally routed transit gateway with VPCs
{: #pricing-example1}

You create a locally routed transit gateway in `us-south` (Dallas) and attach 2 VPCs to it (all in `us-south`). Then, you transfer 2 TB of data between the VPCs this month. Because you have less than 3 monthly connections, there are no connection fees. And because you transferred 2 TB of *local* data, you will be billed at $0.01 USD per GB.

* {{site.data.keyword.tg_full_notm}} connection charge = *FREE*     
* {{site.data.keyword.tg_full_notm}} data transfer charge = *$20 per month* (`2048 GB x $0.01 = $20.48`)

## Example 2: Locally routed transit gateway with VPCs and a classic connection
{: #pricing-example2}

You create a locally routed transit gateway in `us-south` (Dallas) and attach 8 VPCs (all in `us-south`) and 1 classic infrastructure connection, which gives you access to classic resources across MZRs. Then, you transfer a total of 2 TB of data between the VPCs and classic infrastructure networks this month. Because the number of connections is greater than 2 and less than 21, you will be billed $20 per connection this month. 

Also, because you transferred 2 TB of *local* data, you will be billed at $0.01 USD per GB.

* {{site.data.keyword.tg_full_notm}} connection charge (connections 1 & 2) = *$0 per month*
* {{site.data.keyword.tg_full_notm}} connection charge (connections 3 through 9) = *$140 per month*  
* {{site.data.keyword.tg_full_notm}} data transfer charge = *$20.48 per month* (`2,048 GB x $0.01 = $20.48`)

## Example 3: Globally routed transit gateway with VPCs
{: #pricing-example3}

You create a globally routed transit gateway in `us-south` (Dallas) and attach 22 VPCs to it from multiple regions. Then, you transfer a total of 2 TB of data between the VPCs each month. Because the number of connections (22) is greater than 21, and less than 50, you will be billed $15 per connection this month. 

Also, because you selected *global* routing, and a total of 2 TB was sent between the VPCs this month, data transfer is charged at $0.02 per GB.

* {{site.data.keyword.tg_full_notm}} connection charge (connections 1 & 2) = *$0 per month*
* {{site.data.keyword.tg_full_notm}} connection charge (connections 3 through 20) = *$360 per month* 
* {{site.data.keyword.tg_full_notm}} connection charge (connections 21 through 22) = *$30 per month* 
* {{site.data.keyword.tg_full_notm}} data transfer charge = *$40.96 per month* (`2,048 GB x $0.02 = $40.96`)

## Example 4: Globally routed transit gateways with VPCs and classic connections
{: #pricing-example4}

You create two globally routed transit gateways in `us-south` (Dallas) and attach a total of 40 VPCs from multiple regions and 2 classic infrastructure connections, which gives you access to classic resources across MZRs. Then, you transfer a total of 4 TB of data between the VPCs and the classic infrastructure networks this month. Because the number of connections (42) is greater than 21 but less than 50, you will be billed $15 per connection.

Also, because you selected *global* routing, and a total of 4 TB was sent between the VPCs this month, data transfer is charged at $0.02 per GB.

* {{site.data.keyword.tg_full_notm}} connection charge (connections 1 & 2) = *$0 per month*
* {{site.data.keyword.tg_full_notm}} connection charge (connections 3 through 20) = *$360 per month* 
* {{site.data.keyword.tg_full_notm}} connection charge (connections 21 through 42) = *$330 per month* 
* {{site.data.keyword.tg_full_notm}} data transfer charge = *$40.96 per month* (`2,048 GB x $0.02 = $81.92`)
