---

copyright:
  years: 2020, 2025
lastupdated: "2025-06-20"

keywords: editing, managing, manage, edit, add, connection

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Creating a GRE tunnel connection
{: #gre-connection}

You can connect endpoints using a Generic Routing Encapsulation (GRE) tunnel transit gateway connection. This connection allows a transit gateway to connect to overlay networks hosted on classic infrastructure resources.
{: shortdesc}

This form of GRE tunnel is now deprecated, and we suggest using an unbound GRE tunnel instead. Unbound GRE tunnels provide the following benefits:
   * The ability to receive classic network subnets from a classic connection.
   * The ability to communicate through other unbound GRE tunnels on the same transit gateway in the same availability zone.
   * Does not require a classic connection on the transit gateway. As a result, the classic network's subnets will not be advertised to the connections on the transit gateway (and vice versa).
   {: important}

For more information, see [Creating an unbound GRE tunnel](/docs/transit-gateway?topic=transit-gateway-unbound-gre-connection).

Migrating your GRE tunnels to unbound GRE tunnels requires deleting any existing GRE tunnels before creating new unbound ones. Migration will also cause a network disruption for anything that uses the old GRE tunnel until you create the new one.

To migrate from a GRE tunnel to an unbound GRE tunnel:
1. Gather the existing GRE tunnel's configuration information for use on the new unbound GRE tunnel.
1. [Delete your old GRE tunnel](/docs/transit-gateway?topic=transit-gateway-deleting-connections&interface=ui).
1. Delete any classic connections if need be.

   Classic connections can't be deleted if they are being used by other GRE tunnels.
   {: note}

1. [Create the new unbound GRE tunnel](/docs/transit-gateway?topic=transit-gateway-unbound-gre-connection&interface=ui).

Transit gateway GRE connections require the gateway owner to specifically configure HA for their needs. A GRE connection is a point to point connection, has no built in redundancy, and is a single point of failure. When configuring a GRE connection on a transit gateway, you must specify the availability zone. For a robust HA solution, configure multiple GRE connections using different availability zones.
{: note}

## Before you begin
{: #gre-begin}

The following prerequisites must be met before you can create a GRE tunnel connection:

* Ensure that you have an existing classic infrastructure connection, or create one. For more information, see [Adding a connection](/docs/transit-gateway?topic=transit-gateway-adding-connections). The GRE tunnel connection connects with an endpoint only on classic infrastructure.
* Review the [GRE connection considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#gre-considerations) for additional prerequisites.

## Creating a GRE tunnel connection in the UI
{: #tg-ui-adding-gre-connection-transit-gateway}
{: ui}

Only unbound GRE tunnels can be created in the UI. For more information, see [Creating an unbound GRE tunnel](/docs/transit-gateway?topic=transit-gateway-unbound-gre-connection).

## Creating a GRE tunnel connection from the CLI
{: #tg-cli-adding-gre-connection-transit-gateway}
{: cli}

Create a Generic Routing Encapsulation (GRE) tunnel connection on the given transit gateway.

```sh
ibmcloud tg connection-create-gre|ccgre GATEWAY_ID --name NAME --zone ZONE --base-connection-id BASE_CONNECTION_ID --local-gateway-ip LOCAL_GATEWAY_IP --local-tunnel-ip LOCAL_TUNNEL_IP --remote-gateway-ip REMOTE_GATEWAY_IP --remote-tunnel-ip REMOTE_TUNNEL_IP [--remote-bgp-asn REMOTE_BGP_ASN] [--output json]
```
{: pre}

Where:

- **GATEWAY_ID**: ID of the gateway where the new connection is bound.

- **--name**: Name of the new connection.

- **--zone**: Availability zone for the GRE tunnel. Example: `us-south-1`

- **--base-connection-id**: ID of the classic network connection that will be the underlay for the GRE tunnel.

- **--local-gateway-ip**: Local gateway IP address for the GRE tunnel connection.

- **--local-tunnel-ip**: Local tunnel IP address for the GRE tunnel connection.

- **--remote-gateway-ip**: Remote gateway IP address for the GRE tunnel connection.

- **--local-tunnel-ip**: Remote tunnel IP address for the GRE tunnel connection.

- **--remote-bgp-asn**: Optional: If the remote BGP ASN is not specified, one is generated.

- **--output json**: Optional: Shows the output in JSON format.

- **--help | -h**: Optional: Get help on this command.

### Example
{: #connection-create-gre-example}

Create a GRE tunnel connection named `gre-connection` using classic connection `9037f710-8dfb-4948-a2bd-847c8dde96d3` as the base connection:

```sh
ibmcloud tg connection-create-gre $gateway  --name gre-connection --base-connection-id 9037f710-8dfb-9999-a2bd-847c8dde96d3  --zone us-south-2 --local-gateway-ip 192.168.100.1 --local-tunnel-ip 192.168.101.1 --remote-gateway-ip 10.242.63.12 --remote-tunnel-ip 192.168.101.2
```
{: pre}

## Creating a GRE tunnel connection with the API
{: #tg-api-adding-gre-connection-transit-gateway}
{: api}

### Example Request
{: #add-gre-connection-curl-api-request-example}

This example illustrates requesting a GRE connection:

```sh
curl -X POST "https://transit.cloud.ibm.com/v1/transit_gateways/test/connections?version=2022-01-27" -H "accept: application/json" -H "Content-Type: application/json" -d "{\"base_connection_id\":\"975f58c1-afe7-469a-9727-7f3d720f2d32\",\"local_gateway_ip\":\"192.168.100.1\",\"local_tunnel_ip\":\"192.168.129.2\",\"name\":\"Transit_Service_BWTN_SJ_DL\",\"network_type\":\"gre_tunnel\",\"remote_bgp_asn\":65010,\"remote_gateway_ip\":\"10.242.63.12\",\"remote_tunnel_ip\":\"192.168.129.1\"}"
```
{: pre}

The payload for this request is as follows:

```json
{
  "base_connection_id": "975f58c1-afe7-469a-9727-7f3d720f2d32",
  "local_gateway_ip": "192.168.100.1",
  "local_tunnel_ip": "192.168.129.2",
  "name": "Transit_Service_BWTN_SJ_DL",
  "network_type": "gre_tunnel",
  "remote_bgp_asn": 65010,
  "remote_gateway_ip": "10.242.63.12",
  "remote_tunnel_ip": "192.168.129.1"
}
```
{: pre}

### Example Response
{: #add-gre-connection-curl-api-response-example}

This example illustrates the response from creating a GRE tunnel:

```json
{
  "created_at": "2020-03-31T12:08:05Z",
  "id": "1a15dca5-7e33-45e1-b7c5-bc690e569531",
  "name": "example-connection",
  "network_type": "gre_tunnel",
  "status": "pending",
  "updated_at": "2020-03-31T12:08:05Z"
}
```
{: screen}

For more information, see [Adds a connection to a Transit Gateway](/apidocs/transit-gateway?code=java#create-transit-gateway-connection) in the Transit Gateway API reference.
{: note}

## Creating a GRE tunnel connection using Terraform
{: #tg-terraform-adding-gre-connection-transit-gateway}
{: terraform}

You can specify the following argument references for your resource when creating a Generic Routing Encapsulation (GRE) tunnel connection:

|Argument|Details|
|--|--|
|**base_connection_id**  \n Optional  \n Forces new resource  \n string|The ID of a network_type `classic` connection a tunnel is configured over.  \n This field only applies to network type `gre_tunnel` connections.|
|**gateway**  \n Required  \n Forces new resource  \n string|Enter the transit gateway identifier.|
|**local_gateway_ip**  \n Optional  \n Forces new resource  \n string|The local gateway IP address.  \n This field is required for and only applicable to `gre_tunnel` and `unbound_gre_tunnel` connection types.|
|**local_tunnel_ip**  \n Optional  \n Forces new resource  \n string | The local tunnel IP address. \n This field is required for, and only applicable, to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**name**  \n Optional  \n string | Enter a name. If the name is not given, the default name is provided based on the network type, such as `gre_tunnel`. |
|**network_type**  \n Required  \n Forces new resource  \n string | The network type. Allowed values are `gre_tunnel`
|**remote_bgp_asn**  \n Optional  \n Forces new resource  \n integer | The remote network BGP ASN. This will be generated for the connection if not specified.  \n This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**remote_gateway_ip** \n Optional  \n Forces new resource  \n string | The remote gateway IP address. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**remote_tunnel_ip** \n Optional \n Forces new resource  \n string | The remote tunnel IP address. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**zone**  \n Optional \n Forces new resource \n string | The location of the GRE tunnel. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
{: caption="Terraform argument references for creating a GRE" caption-side="bottom"}

### Example
{: #tg-terraform-adding-gre-connection-transit-gateway-example}

This example illustrates requesting a GRE tunnel connection:

```sh
resource "ibm_tg_connection" "test_ibm_tg_connection" {
  gateway            = ibm_tg_gateway.test_tg_gateway.id
  network_type       = "gre_tunnel"
  name               = "myconnection"
  base_connection_id = testgretunnel
  local_gateway_ip   = 192.168.0.1
  local_tunnel_ip    = 10.0.0.1
  remote_bgp_asn     = 36361
  remote_gateway_ip  = 192.168.1.1
  remote_tunnel_ip   = 10.0.1.1
  zone               = us-east
}
```
{: pre}
