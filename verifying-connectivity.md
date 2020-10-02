---

copyright:
  years: 2020
lastupdated: "2020-04-16"

keywords: verifying, connection, connectivity

subcollection: transit-gateway

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
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

# How do I verify and deal with connectivity issues on my transit gatways?
{: #troubleshooting}

There are several issues that can cause problems when attempting to communicate between resources connected to your {{site.data.keyword.tg_full}}.
{: shortdesc}

You may receive error messages that state you need to check whether the resource you are requesting to access exists, and to review your network topology.
{: tsSymptoms}

Known issues include incorrect permissions, overlapping prefixes, networking interface card routing, access control lists, firewalls and gateway appliances, and routing in classic VSIs.
{: tsCauses}

To fix the connectivity issues you're encountering, check that the following items have been set up correctly.
{: tsResolve}

### Checking your permissions
{: #confirm-configuration}

If you are encountering resource issues on the provisioning page, make sure you have the correct [IAM permissions](/docs/transit-gateway?topic=transit-gateway-iam#iam) in order to use {{site.data.keyword.tg_full_notm}} and {{site.data.keyword.cloud_notm}} VPC for the connections you are attempting to make.

If you cannot successfully provision a transit gateway, your account administrator may have disabled certain users' visibility to the [IBM Cloud Catalog](/docs/account?topic=account-accounts#accounts).
{: tip}

### Dealing with overlapping prefixes
{: #overlapping-prefixes}

A common problem when trying to connect networks is that they may have the same prefixes (or overlapping prefixes). This can lead to the same IP address being assigned to multiple resources and cause networking issues. During VPC creation, you set up prefixes and subnets for your private network. You may have chosen the default value, **Default address prefixes**. This is fine when the VPCs exist in isolation. However, when a transit gateway is used to connect these formerly isolated networks, overlaps can occur. If traffic does not appear to be routing to the correct network, this could be the issue.

VPCs created this way do not communicate through a transit gateway because all the traffic stays within the local VPC network. Virtual Machines provisioned on different VPCs with the same IP may appear to ping through the transit gateway, but in reality are just pinging themselves.

When creating VPCs that are intended to be interconnected using a transit gateway, make sure to create the VPCs with non-overlapping prefixes. When creating VPCs that are also intended to be interconnected with your {{site.data.keyword.cloud_notm}} classic infrastructure, do not use IP addresses in your VPCs in the `10.0.0.0/14`, `10.200.0.0/14`, `10.198.0.0/15`, and `10.254.0.0/16` blocks.

### Working with security groups
{: #working-with-security-groups}

[Security Groups](/docs/vpc?topic=vpc-using-security-groups#using-security-groups) exist at the VSI level. Ensure that you allow the protocol you are using to egress from the originator and ingress at the target.

### Working with Network Interface Card routing
{: #nic}

When working with a VSI that has multiple network interface cards (NICs), pay close attention to its networking settings to avoid connectivity problems. These problems may be due to how the routing works in the VSI and its security group. The default route points to the first NIC. In that case, pinging the address of the first NIC may work, however pinging the address of the second NIC may fail. Your security group may block response traffic that is not associated with inbound traffic. As per your needs, you may need to change your default route to configure where to route traffic from all source addresses. Or, you may need to add a route to your routing table to configure where to send traffic from specific source addresses.

### Working with Access Control Lists
{: #acls}

Network Access Control Lists [ACLs](/docs/vpc?topic=vpc-using-acls#using-acls) are applied at the VPC level. By default, they allow all inbound and outbound traffic. Check if you have changed this default.

### Working with firewalls and gateway appliances
{: #firewalls-gateways}

Ensure that a firewall or gateway appliance (such as a [Juniper vSRX](/docs/vsrx?topic=vsrx-getting-started#getting-started)) is not blocking your traffic. For instance, the Juniper vSRX is a firewall appliance that sits between {{site.data.keyword.cloud_notm}} classic infrastructure and the BCR. If you perform a trace route and cannot get to any address at all, then it could be that the vSRX that is blocking the traffic.

### Routing in classic VSIs
{: #routing-classic-vsi}

If you are attempting to access an {{site.data.keyword.cloud_notm}} classic infrastructure VSI that has both a private network interface (`eth0`) and a public network interface (`eth1`), then the issue could be the traffic being routed to the public network interface versus the private. The routing tables for these interfaces point the default gateway to the public interface (`eth1`). Transit gateways are connected only to the private networks. You might have to add entries to route the subnets from other VPCs through the private interface.
