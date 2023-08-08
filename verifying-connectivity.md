---

copyright:
  years: 2023
lastupdated: "2023-02-23"

keywords: verifying, connection, connectivity

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# How do I verify and deal with connectivity issues on my transit gateways?
{: #troubleshooting-connectivity}

There are several issues that can cause problems when attempting to communicate between resources connected to your {{site.data.keyword.tg_full}}.
{: shortdesc}

You may receive error messages that state you need to check whether the resource you are requesting to access exists, and to review your network topology.
{: tsSymptoms}

Known issues include incorrect permissions, overlapping VPC prefixes and classic infrastructure subnets, networking interface card routing, access control lists, firewalls and gateway appliances, and routing in classic VSIs.
{: tsCauses}

To fix the connectivity issues you're encountering, review the following information topics:
{: tsResolve}

* [Connectivity issue basics](/docs/transit-gateway?topic=transit-gateway-connectivity-issue-basics)
* [Working with firewalls and gateway appliances](/docs/transit-gateway?topic=transit-gateway-firewalls-gateways)
* [Dealing with overlapping VPC prefixes and classic infrastructure subnets](/docs/transit-gateway?topic=transit-gateway-overlapping-vpc-prefixes-and-classic-subnets)
* [Working with Network Interface Card Routing](/docs/transit-gateway?topic=transit-gateway-tg-nic)
* [Routing in classic virtual server instances](/docs/transit-gateway?topic=transit-gateway-routing-classic-vsi)
* [GRE tunnel connectivity issues](/docs/transit-gateway?topic=transit-gateway-gre-tunnel-conn-issues)
