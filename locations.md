---

copyright:
  years: 2020, 2026
lastupdated: "2026-08-14"

keywords: about, features, overview

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# IBM Cloud Transit Gateway locations
{: #tg-locations}

{{site.data.keyword.tg_full_notm}} is available in [Multi-Zone Regions (MZR)](#x9774820){: term} worldwide. In addition to MZR-to-MZR connectivity, Transit Gateway can bridge VPC networks to IBM Cloud classic infrastructure in select data centers.
{: shortdesc}

## Transit Gateway deployment locations
{: #table-mzr}

Transit Gateway is deployed in the following {{site.data.keyword.cloud_notm}} [Multi-Zone Regions (MZR)](#x9774820){: term}. A Transit Gateway in any of these regions can connect VPC networks and, where applicable, classic infrastructure.

An MZR consists of three or more independent zones that provide low latency (< 2 ms) and high bandwidth (> 1000 Gbps) connectivity. Deploying across an MZR can raise application availability from 99.9% to 99.99% compared to a single-zone deployment. Any [GA](#x2117947){: term} service available in an MZR becomes available in all MZRs within 90 days.

| Location | Region |
|-----------|----------|
| Dallas | us-south |
| Montreal | ca-mon |
| São Paulo | br-sao |
| Toronto | ca-tor |
| Washington DC | us-east |
{: caption="MZRs in North and South America" caption-side="bottom"}
{: #tg-americas-mzr}
{: tab-title="Americas"}
{: tab-group="mzr"}
{: class="simple-tab-table"}
{: summary="Use the table tabs to change the context of the table. The column headers identify the data centers located in the specific geographical area."}

| Location | Region |
|-----------|----------|
| Frankfurt | eu-de |
| London | eu-gb |
| Madrid | eu-es |
{: caption="MZRs in Europe" caption-side="bottom"}
{: #tg-europe-mzr}
{: tab-title="Europe"}
{: tab-group="mzr"}
{: class="simple-tab-table"}
{: summary="Use the table tabs to change the context of the table. The column headers identify the data centers located in the specific geographical area."}

| Location | Region |
|-----------|----------|
| Chennai - Airtel | in-che |
| Mumbai - Airtel | in-mum |
| Osaka  | jp-osa |
| Sydney | au-syd |
| Tokyo  | jp-tok |
{: caption="MZRs in Asia Pacific" caption-side="bottom"}
{: #tg-asiapacific-mzr}
{: tab-title="Asia Pacific"}
{: tab-group="mzr"}
{: class="simple-tab-table"}
{: summary="Use the table tabs to change the context of the table. The column headers identify the data centers located in the specific geographical area."}

For a detailed overview and list of data centers that are part of each MZR, see [Multizone regions](/docs/overview?topic=overview-locations#table-mzr).
{: note}

## Classic infrastructure data centers in single-zone regions
{: #classic-dc-table}

In addition to connecting VPC networks, a Transit Gateway can connect VPC networks to IBM Cloud classic infrastructure. Classic infrastructure exists in both MZR and single-zone region (SZR) locations. Classic infrastructure in an **MZR** (such as Frankfurt) connects through the Transit Gateway already deployed in that MZR — no separate table entry is needed. The following table covers only the **SZR** classic data centers that support VPC-to-classic connectivity through Transit Gateway.

Classic infrastructure in MZR locations (for example, Frankfurt `eu-de`) is reachable through the Transit Gateway deployed in that MZR. The two tables on this page are intentionally separate: the first shows where Transit Gateway is deployed; this table shows the additional SZR classic data centers that are also reachable.
{: note}

| Location | Data Center |
|-----------|----------|
| Amsterdam | AMS03 |
| Chennai | CHE01 |
| Dallas | DAL09 |
| London | LON02 |
| Montreal | MON01 |
| San Jose | SJC03, SJC04 |
| Singapore | SNG01 |
{: caption="Classic infrastructure data centers that support VPC-to-classic connectivity through Transit Gateway" caption-side="bottom"}
{: #classic-dc-list}
