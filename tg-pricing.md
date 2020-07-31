---

copyright:
  years: 2020
lastupdated: "2020-04-16"

keywords: transit, gateway, about, features, overview

subcollection: transit-gateway

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}
{:term: .term}

# Pricing for IBM Cloud Transit Gateway
{: #tg-pricing}

Get started quickly with a free tier of service for {{site.data.keyword.tg_full}}. Every month, {{site.data.keyword.tg_full_notm}} provides customer accounts 10 free connections, unlimited local data transfer and 1 TB of free data to destinations outside of the gateway’s local region.  

{{site.data.keyword.tg_full_notm}} has two primary billing elements:

1. **Per connection fee pricing** is determined by how many total connections are configured against all provisioned transit gateways **per account**, **per month**. Graduated tier pricing is as follows:

   * Connection #1 to #10 = Free of charge  
   * Connection #11 to #20 =  $20 per connection  
   * Connection #21 to #50 = $15 per connection   
   * Connection #51 and greater = $10 per connection

2. **Data transfer pricing** is determined based on which transit gateway routing option you choose.

   - Local routing: Select this if you need access to IBM Cloud VPC and classic resources within the transit gateway's
region (for example, `us-south`). Data transfer is unlimited and free.

   - Global routing: Choose this if you need to connect IBM Cloud VPCs between [multizone regions](/docs/overview?topic=overview-locations#mzr-table) (for example, between `us-south` and `eu-de`). Data transfer fees are charged at $0.02 per GB for data transfer after the free 1 TB monthly allotment.

   Pricing estimates may vary slightly based on USD currency fluctuations.
   {: note}

   If you ever want to change routing options, you can edit your configuration after you provision your gateway.
   {: tip}

When connecting to resources across accounts, the owner of the transit gateway is responsible for all connection and data transfer fees.

## Pricing examples
{: #pricing-examples}

The following examples describe various pricing scenarios for {{site.data.keyword.tg_full_notm}}.

### Example 1: Locally routed transit gateway with VPCs
{: #example1}

You create a locally routed transit gateway in `us-south` (Dallas) and attach 8 VPCs to it (all in `us-south`). Then, you transfer 2 TB of data between the VPCs this month. Because you have less than 10 monthly connections, there are no connection fees. Also, because you selected local routing, there is no charge for any data transfer between the VPCs.

   * {{site.data.keyword.tg_full_notm}} connection charge = *FREE*     
   * {{site.data.keyword.tg_full_notm}} data transfer charge = *FREE*   

### Example 2: Locally routed transit gateway with VPCs and a classic connection
{: #example2}

You create a locally routed transit gateway in `us-south` (Dallas) and attach 8 VPCs (all in `us-south`) and 1 classic infrastructure connection, which gives you access to classic resources across MZRs. Then, you transfer a total of 2 TB of data between the VPCs and classic infrastructure networks this month. Because you have less than the free allocation of 10 monthly connections, there are no connection fees. Also, because you selected local routing, there is no charge for any data transfer between the VPCs and classic infrastructure.

   * {{site.data.keyword.tg_full_notm}} connection charge = *FREE*     
   * {{site.data.keyword.tg_full_notm}} data transfer charge = *FREE*    

### Example 3: Globally routed transit gateway with VPCs
{: #example3}

You create a globally routed transit gateway in `us-south` (Dallas) and attach 22 VPCs to it from multiple regions. Then, you transfer a total of 2 TB of data between the VPCs each month. Because the number of connections (22) is greater than the free allocation of 10 monthly connections, the next 10 connections are charged at $20 this month, and the remaining 2 connections are charged at $15 per month.

Also, because you selected global routing, and a total of 2 TB was sent between the VPCs this month, data transfer is charged at $0.02 per GB after the 1 TB free allotment.

   * {{site.data.keyword.tg_full_notm}} connection charge = *$230 per month*   
   * {{site.data.keyword.tg_full_notm}} data transfer charge = *$20.48 per month* (`1,024 GB x $0.02 = $20.48`)

### Example 4: Globally routed transit gateway with VPCs and a classic connection
{: #example4}

You create a globally routed transit gateway in `us-south` (Dallas) and attach 22 VPCs from multiple regions and 1 classic infrastructure connection, which gives you access to classic resources across MZRs. Then, you transfer a total of 2 TB of data between the VPCs and the classic infrastructure networks this month. Because the number of connections (23) is greater than the free allocation of 10 monthly connections, the next 10 connections are charged at $20 per month, and the remaining 3 connections are charged at $15.

Also, because you selected global routing, and a total of 2 TB was sent between the VPC and classic infrastructure networks this month, all data transfer (across all VPCs and classic infrastructure networks alike) is charged at $0.02 per GB after the 1 TB free allotment each month.

   * {{site.data.keyword.tg_full_notm}} connection charge = *$245 per month*   
   * {{site.data.keyword.tg_full_notm}} data transfer charge = *$20.48 per month* (`1,024 GB x $0.02 = $20.48`)
