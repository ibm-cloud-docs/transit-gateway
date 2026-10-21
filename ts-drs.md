---

copyright:
  years: 2026, 2026
lastupdated: "2026-10-21"

keywords: dynamic route server, DRS, troubleshoot, connection failed

subcollection: transit-gateway

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does my dynamic route server fail to connect to the transit gateway? (beta)
{: #troubleshoot-drs}
{: troubleshoot}
{: support}

[Dynamic Route Server for VPC is a beta feature](/docs/transit-gateway?topic=transit-gateway-transit-gateway-release-notes#transit-gateway-drs) that is available for evaluation and testing purposes to select customers. Access is restricted to allowlisted accounts.
{: beta}

Dynamic route server connection creation can fail for several reasons, including missing prerequisites or unsupported parameters. This topic lists common error messages and how to resolve them.
{: shortdesc}

When you create a dynamic route server connection to a transit gateway, the request fails. Possible error messages include:
{: tsSymptoms}

* `The VPC hosting this Dynamic Route Server must also be connected to this transit gateway.`
* `The Dynamic Route Server is not in a stable state. Ensure the DRS lifecycle_state is stable and health_state is healthy, then try again.`
* `Dynamic Route Server ASN conflicts with a Transit Gateway reserved ASN. Update the DRS ASN and retry.`
* `Tunnel IP range overlaps with Dynamic Route Server appliance subnets. Specify a non-overlapping CIDR block.`
* `Tunnel IP CIDR overlaps with an existing connection CIDR on this transit gateway. Specify a non-overlapping CIDR block.`
* `--zone option is ignored for Dynamic Route Server connections.`
* `--default-prefix-filter option cannot be used with Dynamic Route Server connections.`
* `Prefix filters are not supported on Dynamic Route Server connections.`
* `This Dynamic Route Server is already connected to a transit gateway. Remove the existing connection before attaching to a new gateway.`

These errors occur because one or more prerequisites are not met, or because unsupported parameters were specified:
{: tsCauses}

* The VPC that hosts the dynamic route server is not connected to the transit gateway.
* The dynamic route server is not in `Stable` lifecycle state or does not have `Healthy` health status.
* The dynamic route server ASN conflicts with a Transit Gateway reserved ASN.
* The CIDR block overlaps with dynamic route server appliance VNI subnets or with another connection CIDR on the transit gateway.
* The `--zone` flag was specified, which is not supported for dynamic route server connections.
* The `--default-prefix-filter` flag was specified, which is not supported for dynamic route server connections.
* A prefix filter was added to a dynamic route server connection, which is not supported.
* The dynamic route server is already attached to another transit gateway.

To resolve these issues:
{: tsResolve}

1. **Verify the dynamic route server host VPC is connected.** The VPC that hosts the dynamic route server must also be connected to the same transit gateway. Add a VPC connection for that VPC before creating the dynamic route server connection.

1. **Verify dynamic route server state.** Confirm that the dynamic route server instance has lifecycle state `Stable` and health status `Healthy`. If it does not, wait for the dynamic route server to reach a stable and healthy state before retrying.

1. **Resolve ASN conflicts.** If the dynamic route server ASN conflicts with a Transit Gateway reserved ASN, update the dynamic route server ASN to a non-reserved value and retry. For the list of reserved ASNs, see [Dynamic route server connection considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#drs-connection-considerations).

1. **Use a non-overlapping CIDR.** Ensure the CIDR you provide does not overlap with the subnets where dynamic route server appliance VNIs are deployed, and does not overlap with any other connection CIDR already configured on the transit gateway.

1. **Remove unsupported parameters.** Do not specify `--zone` or `--default-prefix-filter` when creating a dynamic route server connection. Remove these parameters from your request and retry.

1. **Do not add prefix filters.** Prefix filtering is not supported on dynamic route server connections. Remove any prefix filter creation requests targeting a dynamic route server connection.

1. **Check existing attachments.** In the current release, a dynamic route server can be connected to only one transit gateway at a time. If the dynamic route server is already attached to another transit gateway, delete that connection before creating a new one.
