---

copyright:
  years: 2020
lastupdated: "2020-05-26"

keywords: transit, gateway, about, features, overview

subcollection: transit-gateway

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank_"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}
{:term: .term}

# IBM Cloud Transit Gateway Multi-Zone Region locations
{: #tg-locations}

A [Multi-Zone Region (MZR)](#x9774820){: term} is comprised of 3 or more zones that are independent from each other to ensure that single failure events affect only a single zone. MZRs provide low latency (< 2 milliseconds latency) and high bandwidth (> 1000 Gbps) connectivity across zones. Any [GA](#x2117947){: term} service in an MZR will be available in all MZRs within 90 days. 

The advantage of an MZR is that it provides consistent cloud services across different zones, better resiliency, availability, higher interconnect speed between data centers for your resources. These features can be critical to your applications. Deploying the application in an MZR rather than a SZR can increase the availability from 99.9% to 99.99% when deployed over 3 zones. 

{{site.data.keyword.tg_full_notm}} is currently deployed within the following {{site.data.keyword.cloud_notm}} Multi-Zone Regions (MZR):

| Location | Region |
|-----------|----------|
| Dallas | us-south |
| Washington DC | us-east |
{: caption="Table 1. MZRs in North and South America" caption-side="top"}
{: #tg-americas-mzr}
{: tab-title="Americas"}
{: tab-group="mzr"}
{: class="simple-tab-table"}
{: summary="Use the buttons before the table to change the context of the table. The column headers identify the data centers located in the specific geographical area."}

| Location      | Region   |
|-----------|----------|
| Frankfurt     | eu-de    |
| London        | eu-gb    |
{: caption="Table 1. MZRs in Europe" caption-side="top"}
{: #tg-europe-mzr}
{: tab-title="Europe"}
{: tab-group="mzr"}
{: class="simple-tab-table"}
{: summary="Use the buttons before the table to change the context of the table. The column headers identify the data centers located in the specific geographical area."}

| Location      | Region   |
|-----------|----------|
| Sydney        | au-syd   |
| Tokyo         | jp-tok   |
{: caption="Table 1. MZRs in Asia Pacific" caption-side="top"}
{: #tg-asiapacific-mzr}
{: tab-title="Asia Pacific"}
{: tab-group="mzr"}
{: class="simple-tab-table"}
{: summary="Use the buttons before the table to change the context of the table. The column headers identify the data centers located in the specific geographical area."}
