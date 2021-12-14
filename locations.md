---

copyright:
  years: 2020
lastupdated: "2020-09-28"

keywords: about, features, overview

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# IBM Cloud Transit Gateway locations
{: #tg-locations}

You can interconnect {{site.data.keyword.cloud}} classic and Virtual Private Cloud (VPC) infrastructures worldwide using [Multi-Zone Regions (MZR)](#x9774820){: term} and [Single-Zone Regions (SZR)](#x9774825){: term}.
{: shortdesc}

## Multi-Zone Regions
{: #mzr-table}

An MZR consists of three or more zones that are independent from each other to ensure that single failure events affect only a single zone. MZRs provide low latency (< 2-milliseconds latency) and high bandwidth (> 1000 Gbps) connectivity across zones. Any [GA](#x2117947){: term} service in an MZR will be available in all MZRs within 90 days.

An MZR provides consistent cloud services across different zones, better resiliency, availability, and higher interconnect speed between data centers for your resources. These features can be critical to your applications. Deploying the application in an MZR rather than an SZR can increase the availability from 99.9% to 99.99% when deployed over three zones.

{{site.data.keyword.tg_full_notm}} is currently deployed within the following {{site.data.keyword.cloud_notm}} MZRs:

| Location | Region |
|-----------|----------|
| Dallas | us-south |
| San Paulo | br-sao |
| Toronto | ca-tor |
| Washington DC | us-east |
{: caption="Table 1. MZRs in North and South America" caption-side="bottom"}
{: #tg-americas-mzr}
{: tab-title="Americas"}
{: tab-group="mzr"}
{: class="simple-tab-table"}
{: summary="Use the table tabs to change the context of the table. The column headers identify the data centers located in the specific geographical area."}

| Location | Region |
|-----------|----------|
| Frankfurt | eu-de |
| London | eu-gb |
{: caption="Table 1. MZRs in Europe" caption-side="bottom"}
{: #tg-europe-mzr}
{: tab-title="Europe"}
{: tab-group="mzr"}
{: class="simple-tab-table"}
{: summary="Use the table tabs to change the context of the table. The column headers identify the data centers located in the specific geographical area."}

| Location | Region |
|-----------|----------|
| Osaka  | jp-osa |
| Sydney | au-syd |
| Tokyo  | jp-tok |
{: caption="Table 1. MZRs in Asia Pacific" caption-side="bottom"}
{: #tg-asiapacific-mzr}
{: tab-title="Asia Pacific"}
{: tab-group="mzr"}
{: class="simple-tab-table"}
{: summary="Use the table tabs to change the context of the table. The column headers identify the data centers located in the specific geographical area."}

For a detailed overview and list of data centers that are part of the MZR, see [Multizone regions](/docs/overview?topic=overview-locations#mzr-table).
{: note}

## Single-Zone Regions
{: #szr-table}

You can establish connectivity from a VPC to resources in an SZR by connecting both the VPC and classic infrastructure to a transit gateway. The following table lists the SZRs in {{site.data.keyword.cloud_notm}} for interconnecting classic infrastructure to VPCs using a transit gateway.

| Location | Data Center |
|-----------|----------|
| Dallas | DAL09 |
| London | LON02 |
| Montreal | MON01 |
| San Jose | SJC04 |
| Seoul | SEO01 |
{: caption="Table 2. SZRs for classic Softlayer IaaS" caption-side="bottom"}
