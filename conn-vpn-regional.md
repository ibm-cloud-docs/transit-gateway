---

copyright:
  years: 2026, 2026
lastupdated: "2026-08-31"

keywords: VPN gateway, regional VPN, regional connection, zone failover, spoke

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

[New]{: tag-new}
<regional>

# Connecting a regional VPN gateway
{: #vpn-regional-connection}

**Regional:** This feature is available to allowlisted accounts only. Contact IBM Support to request access.
{: note}

You can attach a regional VPN gateway to a transit gateway as a spoke connection. A regional VPN gateway provides zone-level resiliency by deploying two VPN appliances in separate zones within the same region. If one zone becomes unavailable, traffic automatically fails over to the appliance in the healthy zone—without requiring you to create multiple VPN gateways or specify a zone when creating the connection.
{: shortdesc}

Unlike a zonal VPN connection, a regional VPN connection does not require an availability zone as an input. The zone for each tunnel is derived automatically from the VPN gateway's member configuration. For more information, including a zone layout and a comparison of zonal and regional gateways, see [VPN gateway overview](/docs/vpc?topic=vpc-using-vpn#regional-vpn-gateway).

## Before you begin
{: #vpn-regional-connection-prereqs}

Before you connect a regional VPN gateway to a transit gateway, make sure that:

- Your VPN gateway is configured with `availability_mode` set to `regional` and uses route-based mode (`mode: route`).
- Your VPN gateway has a non-zero `local_asn` (Autonomous System Number). Reserved ASNs cannot be used, including: `0`, `13884`, `36351`, `64512`, `64513`, `65100`, `65200–65234`, `65402–65433`, `65500`, `65516`, `65519`, `65521`, `65531`, and `4201065000–4201065999`.
- Your VPN gateway is in `stable` lifecycle state.
- You have a CIDR block available for the GRE tunnel IP addresses. The CIDR must:
   - Use [RFC 1918](https://datatracker.ietf.org/doc/html/rfc1918){: external} private address space.
   - Be at least a `/27` subnet.
   - Not overlap with VPN member subnets or other connection CIDRs on the transit gateway.

If no CIDR is specified, the default range `198.19.174.0/23` is used.
{: note}

For more information about VPN gateway planning requirements, see [Planning considerations for VPN gateways](/docs/vpc?topic=vpc-planning-considerations-vpn).

## Creating a regional VPN connection in the UI
{: #vpn-regional-connection-ui}
{: ui}

To connect a regional VPN gateway to a transit gateway in the UI, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**.
1. Click the name of the transit gateway where you want to add a connection, then click **Add connection**.
1. For **Network connection**, select **VPN gateway**.
1. Choose a connection reach option:

   * **Add new connection in this account** — Select the region where the VPN gateway is deployed, then select from the list of available regional VPN gateways. Only VPN gateways that use dynamic routing (`route` mode) are shown.

      The zone field is not available for regional VPN gateways. Zone selection is automatic.
      {: note}

   * **Request connection to a network in another account** — Enter the Cloud Resource Name (CRN) of the VPN gateway.

1. Optionally, specify a custom CIDR block for the tunnel IP addresses. If left blank, the default range `198.19.174.0/23` is used.
1. Enter a connection name, then click **Add**.

The connection status changes to **Attached** when the redundant GRE tunnels are provisioned and eBGP sessions are established.

## Creating a regional VPN connection from the CLI
{: #vpn-regional-connection-cli}
{: cli}

To connect a regional VPN gateway from the CLI, enter the following command:

```sh
ibmcloud tg connection-create|cc GATEWAY_ID \
  --name NAME \
  --network-id VPN_GATEWAY_CRN \
  --network-type vpn_gateway \
  [--cidr CIDR] \
  [--output json]
```
{: pre}

Do not specify `--zone` for a regional VPN gateway connection. Zone selection is automatic.
{: important}

Where:

`GATEWAY_ID`
:   ID of the transit gateway.

`--name`
:   Name for the new connection.

`--network-id`
:   CRN of the regional VPN gateway.

`--network-type vpn_gateway`
:   Specifies a VPN gateway connection.

`--cidr`
:   Optional: CIDR block for GRE tunnel IP addresses. Must be at least a `/27` subnet using RFC 1918 private address space and must not overlap with other connection CIDRs on the transit gateway. If not specified, `198.19.174.0/23` is used.

### Example
{: #vpn-regional-connection-cli-example}

```sh
ibmcloud tg cc $GATEWAY_ID \
  --name regional-vpn-conn \
  --network-id $VPN_GATEWAY_CRN \
  --network-type vpn_gateway \
  --cidr 192.168.100.0/27
```
{: pre}

## Creating a regional VPN connection with the API
{: #vpn-regional-connection-api}
{: api}

To create a regional VPN connection with the API:

```sh
curl -X POST --location --header "Authorization: Bearer {iam_token}" \
  --header "Accept: application/json" \
  --header "Content-Type: application/json" \
  --data '{
    "name": "regional-vpn-conn",
    "network_type": "vpn_gateway",
    "network_id": "{vpn_gateway_crn}",
    "tunnel_ip_cidr": "192.168.100.0/27"
  }' \
  "{base_url}/transit_gateways/{transit_gateway_id}/connections?version={version}"
```
{: pre}

Do not include a `zone` property in the request body for a regional VPN connection. Zone selection is derived automatically from the VPN gateway member configuration.
{: important}

For more information, see [Create a connection](/docs/apis/transit-gateway?code=java#create-transit-gateway-connection) in the Transit Gateway API reference.
{: note}

## Considerations for regional VPN connections
{: #vpn-regional-connection-considerations}

- **Zone is automatic.** You cannot specify a zone when connecting a regional VPN gateway. Each tunnel is placed on Transit Gateway routers in the zone that corresponds to the VPN member's zone. For more information, see [Planning considerations for VPN gateways](/docs/vpc?topic=vpc-planning-considerations-vpn) and [Use case 9: Zone-resilient VPN connectivity](/docs/vpc?topic=vpc-using-vpn#use-case-9-vpn).
- **Two appliances, two zones.** The transit gateway creates two sets of redundant GRE tunnels—one set per VPN appliance—distributed across the appliances' zones. Each zone gets two tunnels on separate Transit Gateway routers.
- **Automatic GRE tunnel updates.** When a regional VPN gateway member is moved to a new subnet—changing its zone or private IP address—the VPN service automatically notifies the connected transit gateway. The transit gateway then updates its GRE tunnels to reflect the new appliance location. No manual action is required on the transit gateway side. For more information, see [Updating a regional VPN gateway member](/docs/vpc?topic=vpc-vpn-update-regional-member) and [HA with a regional gateway](/docs/vpc?topic=vpc-vpn-ha#vpn-ha-regional).
- **Failover is automatic.** If a zone fails, the VPN appliance in the healthy zone continues routing traffic. BGP sessions for the failed appliance are withdrawn, and the healthy appliance takes over within BGP convergence time. For more information, see [HA with a regional gateway](/docs/vpc?topic=vpc-vpn-ha#vpn-ha-regional).
- **Cross-zone latency.** If a VPN appliance in one zone handles traffic for a workload in another zone, the traffic traverses the IBM Cloud backbone network between zones, adding minimal latency.
- **One connection per VPN gateway.** A VPN gateway can be attached to only one transit gateway at a time.
- **Route propagation.** To maintain high availability across GRE connections, enable [GRE enhanced route propagation](/docs/transit-gateway?topic=transit-gateway-helpful-tips#gre-enhanced-route-propagation-considerations) on the transit gateway.
- **Migration from zonal to regional.** Migration of an existing zonal VPN to a regional VPN is available for SAP enterprise accounts only. For all other accounts, create a new regional VPN gateway. For more information, contact IBM Support.

</regional>
