---

copyright:
  years: 2026, 2026
lastupdated: "2026-10-21"

keywords: dynamic route server, BGP, GRE, connection, spoke

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Connecting a dynamic route server (beta)
{: #drs-connection}

[Dynamic Route Server for VPC is a beta feature](/docs/transit-gateway?topic=transit-gateway-transit-gateway-release-notes#transit-gateway-drs) that is available for evaluation and testing purposes to select customers. Access is restricted to allowlisted accounts.
{: beta}

You can attach a VPC dynamic route server to a transit gateway as a spoke connection. A dynamic route server peers with routers using BGP to dynamically update VPC routing tables. When you connect a dynamic route server to a transit gateway, the transit gateway establishes redundant GRE tunnels to the dynamic route server appliances and runs eBGP sessions over those tunnels. The dynamic route server learns routes from the transit gateway but does not carry data-path traffic.
{: shortdesc}

## Before you begin
{: #drs-connection-prereqs}

Review [Dynamic route server connection considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#drs-connection-considerations) before you proceed. These considerations cover CIDR requirements, zone placement, prefix filter restrictions, tunnel quotas, and other constraints that affect whether the connection can be created successfully.
{: important}

Before you connect a dynamic route server to a transit gateway, make sure that:

- The dynamic route server instance is in `Stable` lifecycle state with `Healthy` health status.
- The VPC hosting the dynamic route server is **already connected** to the transit gateway. The VPC/Transit Gateway connection must exist before the dynamic route server connection can be created.
- The dynamic route server ASN does not conflict with any transit gateway reserved ASN.
- If you want to specify a CIDR block for GRE tunnel IP addresses, one is available that meets the requirements in [Dynamic route server connection considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#drs-connection-considerations). If not specified, a sub-range is automatically allocated from the default pool.
- For cross-account connections, obtain the CRN of the dynamic route server instance from the account that owns it.

When you later delete this connection, the dynamic route server connection must be fully deleted before the VPC/Transit Gateway connection can be removed. In a cross-account scenario, coordinate with the gateway owner if the dynamic route server connection shows a `Detached` state. For more information, see [Dynamic route server deletion considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#drs-deletion-considerations).
{: important}

## Creating a dynamic route server connection in the UI
{: #drs-connection-ui}
{: ui}

To connect a dynamic route server to a transit gateway in the UI, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**.
1. Click the name of the transit gateway where you want to add a connection, then click **Add connection**.
1. For **Network connection**, select **Dynamic Route Server**.
1. Choose a connection reach option:

   * **Add new connection in this account** — Select the region where the dynamic route server is deployed, then select the dynamic route server from the **Available connections** list. The **Connection name** field is pre-populated with the dynamic route server name. Optionally, enter a CIDR in the **Network (optional)** field for the GRE tunnel IP addresses. If left blank, the default range `198.19.174.0/23` is used.

   * **Request connection to a network in another account** — Enter the CRN of the dynamic route server in the **Dynamic Route Server CRN** field. Enter a **Connection name**. Optionally, enter a CIDR in the **Network (optional)** field.

      After you submit the request, the network owner must approve the connection within 72 hours, or the request expires.
      {: note}

1. Click **Create**.

After the connection is established, you can click the network name in the connections table to open the **Connected Dynamic Route Server details** panel. This panel shows the dynamic route server name, CRN, ID, creation date, and health state. Click **View full Dynamic Route Server details** to navigate to the dynamic route server resource in the VPC console.

## Creating a dynamic route server connection from the CLI
{: #drs-connection-cli}
{: cli}

To connect a dynamic route server from the CLI, enter the following command:

```sh
ibmcloud tg connection-create GATEWAY_ID \
  --name NAME \
  --network-type dynamic_route_server \
  --network-id DRS_CRN \
  [--cidr CIDR] \
  [--output json]
```
{: pre}

Where:

`GATEWAY_ID`
:   ID of the transit gateway.

`--name`
:   Name for the new connection.

`--network-id`
:   CRN of the dynamic route server.

`--network-type dynamic_route_server`
:   Specifies a dynamic route server connection.

`--cidr`
:   Optional: CIDR block for GRE tunnel IP addresses. Must be at least a `/26` subnet using RFC 1918 private address space and must not overlap with dynamic route server appliance VNI subnets or other connection CIDRs on the transit gateway. If not specified, the default range `198.19.174.0/23` is used.

The `--zone` and `--default-prefix-filter` flags are not supported for dynamic route server connections. The `--zone` flag is ignored if specified, while specifying `--default-prefix-filter` returns an error.
{: note}

### Examples
{: #drs-connection-cli-examples}

Create a connection without a CIDR:

```sh
ibmcloud tg connection-create $GATEWAY_ID \
  --name drs-test-no-cidr \
  --network-type dynamic_route_server \
  --network-id $DRS_CRN
```
{: pre}

Create a connection with an explicit CIDR:

```sh
ibmcloud tg connection-create $GATEWAY_ID \
  --name drs-test-with-cidr \
  --network-type dynamic_route_server \
  --network-id $DRS_CRN \
  --cidr 198.19.176.0/23
```
{: pre}

## Creating a dynamic route server connection with the API
{: #drs-connection-api}
{: api}

To create a dynamic route server connection with the API:

```sh
curl -X POST --location --header "Authorization: Bearer {iam_token}" \
  --header "Accept: application/json" \
  --header "Content-Type: application/json" \
  --data '{
    "name": "my-drs-connection",
    "network_type": "dynamic_route_server",
    "network_id": "{drs_crn}",
    "cidr": "198.19.176.0/23"
  }'   "{base_url}/transit_gateways/{transit_gateway_id}/connections?version={version}"
```
{: pre}

Omit `cidr` to use the default range `198.19.174.0/23`.
{: note}

For more information, see [Create a connection](/docs/apis/transit-gateway?code=java#create-transit-gateway-connection) in the Transit Gateway API reference.
{: note}

## Creating a dynamic route server connection with Terraform
{: #drs-connection-terraform}
{: terraform}

To create a dynamic route server connection with Terraform:

```terraform
resource "ibm_tg_connection" "drs_connection" {
  gateway      = ibm_tg_gateway.my_tg_gateway.id
  network_type = "dynamic_route_server"
  name         = "my-drs-connection"
  cidr         = "198.19.176.0/23"
  network_id   = ibm_is_drs.my_drs.crn
}
```
{: codeblock}

For more information, see the [ibm_tg_connection](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/tg_connection){: external} Terraform reference.

## Next steps
{: #drs-connection-next-steps}

- [Generate a route report](/docs/transit-gateway?topic=transit-gateway-route-reports) to verify that routes are being learned correctly across the dynamic route server connection.
- Review [Planning considerations for dynamic route servers](/docs/vpc?topic=vpc-planning-drs) in the VPC documentation to configure peer groups and routing policies on the dynamic route server itself.
- To monitor health and diagnose issues with the connection, see [Diagnosing dynamic route server health](/docs/vpc?topic=vpc-drs-health) in the VPC documentation.
