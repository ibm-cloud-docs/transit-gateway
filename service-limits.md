---

copyright:
  years: 2020, 2026
lastupdated: "2026-09-02"

keywords: service limits, quotas, connections, prefixes, GRE tunnels, transit gateway

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Quotas and service limits
{: #service-limits}

{{site.data.keyword.tg_full_notm}} enforces quotas and service limits on the resources that you can create. These limits are set per account or per gateway and represent the maximum values supported in the current release.
{: shortdesc}

| Service limit |  Default |
|---------------------------|------|
| Number of transit gateways | 10 gateways per account, 5 gateways per region |
| Number of connections per transit gateway | * 10 IBM Cloud VPC connections  \n * 5 IBM Cloud classic connections  \n * 5 IBM Cloud Direct Link connections  \n * 5 {{site.data.keyword.powerSys_notm}} connections |
| Number of prefixes per connection | * 50 prefixes for VPC connections  \n * 120 prefixes for classic connections  \n * 120 prefixes for GRE connections  \n * 120 prefixes for Direct Link connections  \n * 120 prefixes for {{site.data.keyword.powerSys_notm}} connections |
| Number of connections with prefix filters | 2 connections with prefix filters per gateway |
| Number of prefix filters per connection | 10 prefix filters per connection |
| Number of GRE tunnels per transit gateway | 12 GRE tunnels per gateway |
| Number of unique base networks targeted by unbound GRE tunnels per transit gateway | 5 unique base networks targeted by unbound GRE tunnels per gateway |
{: caption="IBM Cloud Transit Gateway service limits" caption-side="bottom"}

You can open an [IBM Support case](/docs/support?topic=support-open-case&interface=ui) if you need your service limits expanded.
{: note}
