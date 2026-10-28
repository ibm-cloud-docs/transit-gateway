---

copyright:
  years: 2026, 2026
lastupdated: "2026-10-27"

keywords: VPN gateway, regional VPN, connection pending, connection error, troubleshoot

subcollection: transit-gateway

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my regional VPN gateway connection stuck in pending or error state?
{: #troubleshoot-regional-vpn-pending}
{: troubleshoot}
{: support}

After you create a VPN gateway connection to a transit gateway using a regional VPN gateway, the connection status remains `pending` for longer than expected or transitions to `error`.
{: tsSymptoms}

A regional VPN connection requires the transit gateway to establish redundant GRE tunnels to both VPN appliances, one per zone. The connection status changes to `attached` only after the transit gateway provisions all tunnels and establishes eBGP sessions with the VPN appliances.

The connection may stay in `pending` or move to `error` for the following reasons:
{: tsCauses}

- The VPN gateway is not in `stable` lifecycle state when the connection is created.
- The CIDR block you specified for the GRE tunnel IP addresses overlaps with one of the VPN member subnets or with another connection CIDR on the transit gateway.
- The VPN gateway's ASN matches a reserved ASN that the transit gateway does not allow: `0`, `13884`, `36351`, `64512`, `64513`, `65100`, `65200–65234`, `65402–65433`, `65500`, `65516`, `65519`, `65521`, `65531`, or `4201065000–4201065999`.
- The VPN gateway is already attached to another transit gateway. A regional VPN gateway can be connected to only one transit gateway at a time.

To resolve this issue:
{: tsResolve}

1. Check the lifecycle state of your VPN gateway. The gateway must be in `stable` state before a transit gateway connection can be created. If the VPN gateway is still provisioning or in a degraded state, wait until it is stable and try again.

1. Verify that your CIDR block does not overlap with the VPN member subnets. To find the member subnets, check the VPN gateway details page or run:

   ```sh
   ibmcloud is vpn-gateway VPN_GATEWAY_ID --output json
   ```
   {: pre}

   If an overlap exists, delete the connection and re-create it with a non-overlapping CIDR block.

1. Confirm that the VPN gateway's `local_asn` is not a reserved ASN. If it is, you must update the ASN on the VPN gateway, delete the transit gateway connection, and re-create it.

1. Check whether the VPN gateway is already connected to another transit gateway. If it is, you must delete that connection before creating a new one.

1. If the connection status is `error`, delete the connection and re-create it after resolving the applicable issue.

For more information, see [Regional VPN gateway considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#regional-vpn-connection-considerations) and [Connecting a regional VPN gateway](/docs/transit-gateway?topic=transit-gateway-vpn-regional-connection).
