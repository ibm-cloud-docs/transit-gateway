---

copyright:
  years: 2020
lastupdated: "2023-02-23"

keywords: verifying, connection, connectivity

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Dealing with overlapping VPC prefixes and classic infrastructure subnets
{: #overlapping-vpc-prefixes-and-classic-subnets}

A common problem when trying to connect networks is that they may have overlapping VPC prefixes and classic infrastructure subnets. During VPC creation, you set up prefixes and subnets for your private network. You may have chosen the default value, **Default address prefixes**. This is fine when the VPCs exist in isolation. However, when a transit gateway is used to connect these formerly isolated networks and the networks have VPC prefixes and classic infrastructure subnets that overlap, this can cause networking issues. If traffic does not appear to be routing to the correct network, this could be the issue.

VPCs created this way do not communicate through a transit gateway because all the traffic stays within the local VPC network. Virtual Machines provisioned on different VPCs with the same IP may appear to ping through the transit gateway, but in reality are just pinging themselves.

When creating VPCs that are intended to be interconnected using a transit gateway, make sure to create the VPCs with non-overlapping VPC prefixes. When creating VPCs that are also intended to be interconnected with your {{site.data.keyword.cloud_notm}} classic infrastructure, do not use prefixes in your VPCs that overlap with the `10.0.0.0/14`, `10.200.0.0/14`, `10.198.0.0/15`, and `10.254.0.0/16` blocks. Also, don't use addresses from your classic infrastructure subnets. To view a list of your classic infrastructure subnets, see [View all subnets](/docs/subnets?topic=subnets-view-all-subnets).
