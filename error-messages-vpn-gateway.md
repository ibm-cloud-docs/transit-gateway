---

copyright:
  years: 2025
lastupdated: "2025-11-04"

keywords: overlapping routes

subcollection: transit-gateway

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does my VPN gateway fail to connect to the transit gateway?
{: #troubleshoot-vpn-gateway}
{: troubleshoot}
{: support}

VPN connection creation can fail if tunnel IPs, subnets, or connection settings conflict. This topic helps identify the common causes and steps to resolve these issues.
{: shortdesc}

When creating a VPN connection to a transit gateway, the request fails with a `400 Bad Request` error. Possible error messages include:
{: tsSymptoms}

* `Invalid VPN gateway connection mode.`
* `Tunnel IP range overlaps with VPN gateway subnets. Specify a non-overlapping CIDR block.`
* `Tunnel IPs overlap with VPN gateway connection tunnel IPs. Specify a valid CIDR block.`
* `Tunnel IP overlaps with the VPN gateway peer address. Specify a different CIDR block.`

These errors typically occur due to misconfigurations in the VPN connection setup, including:
{: tsCauses}

* Unsupported or incorrect VPN gateway connection mode.
* Tunnel IP range overlaps with VPN gateway subnets or existing tunnel IPs.
* Tunnel IP overlaps with the peer address.

To resolve these issues, check all the tunnel IPs and the provided configuration, and select non-overlapping CIDR blocks.
{: tsResolve} 
