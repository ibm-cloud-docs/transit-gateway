---

copyright:
  years: 2023
lastupdated: "2023-02-23"

keywords:

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Connectivity issue basics
{: #connectivity-basics}

There are several simple issues that might be causing your connectivity issues. Verify the following tasks to eliminate them as problems.

## Checking your permissions
{: #confirm-configuration}

If you are encountering resource issues on the provisioning page, make sure you have the correct [IAM permissions](/docs/transit-gateway?topic=transit-gateway-iam) in order to use {{site.data.keyword.tg_full_notm}} and {{site.data.keyword.cloud_notm}} VPC for the connections you are attempting to make.

If you cannot successfully provision a transit gateway, your account administrator may have disabled certain users' visibility to the [IBM Cloud catalog](/docs/account?topic=account-accounts#accounts).
{: tip}

## Using supported locations
{: #confirm-locations}

If you are not able to establish connectivity between networks interconnected by a transit gateway, ensure that your networks are located in one of the [Transit gateway supported locations](/docs/transit-gateway?topic=transit-gateway-tg-locations). You will not be able to establish connectivity to a resource in an unsupported location.

## Working with security groups
{: #working-with-security-groups}

[Security groups](/docs/vpc?topic=vpc-using-security-groups#using-security-groups) exist at the VSI level. Ensure that you allow the protocol you are using to egress from the originator and ingress at the target.

## Working with Access Control Lists
{: #acls}

Network Access Control Lists [ACLs](/docs/vpc?topic=vpc-using-acls#using-acls) are applied at the VPC level. By default, they allow all inbound and outbound traffic. Check if you have changed this default.

## Interconnecting VPCs
{: #interconnecting-vpcs}

You can create a single transit gateway or multiple transit gateways to interconnect more than one IBM Cloud VPCs. You can also connect your IBM Cloud classic infrastructure to a transit gateway to provide seamless communication with classic infrastructure resources. For more information, refer to [Interconnecting VPCs](/docs/vpc?topic=vpc-interconnectivity&interface=cli#interconnecting-vpcs).
