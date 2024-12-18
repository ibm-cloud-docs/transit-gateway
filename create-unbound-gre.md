---

copyright:
  years: 2020, 2024
lastupdated: "2024-12-18"

keywords: editing, managing, manage, edit, add, connection

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Creating an unbound GRE tunnel
{: #unbound-gre-connection}

You can use an unbound Generic Routing Encapsulation (GRE) tunnel transit gateway connection to connect endpoints. This connection allows a transit gateway to connect to overlay networks hosted on classic infrastructure resources.
{: shortdesc}

## Before you begin
{: #unbound-gre-begin}

Before creating an unbound GRE tunnel, review
[GRE connection considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#gre-considerations)
for additional prerequisites.

Unbound transit gateway GRE connections require the gateway owner to specifically configure HA for their needs. A GRE connection is a point-to-point connection, has no built in redundancy, and is a single point of failure. When configuring an unbound GRE tunnel on a transit gateway, you must specify the availability zone. For a robust HA solution, configure multiple GRE connections using different availability zones.
{: important}

Keep in mind that you are required to enter four IP addresses when you create an unbound GRE tunnel. These are:

* **Remote gateway IP** - the IP address of your GRE tunnel endpoint. This IP address must be a private IP and be the private IP from the classic environment. For example, this IP can be a hardware appliance or even a VM.
* **Local gateway IP** - the IP address that your tunnel endpoint connects to. This IP is the transit gateway's IP for the purpose of establishing the tunnel so that when you enter the "remote IP" on your tunnel endpoint, you use this IP address.
* **Remote tunnel IP** - the GRE tunnel address on the tunnel endpoint.
* **Local tunnel IP** - the GRE tunnel address on the transit gateway side.

## Creating an unbound GRE tunnel in the UI
{: #tg-ui-adding-unbound-gre-connection-transit-gateway}
{: ui}

You can create an unbound GRE tunnel on an existing transit gateway, or when you are creating a new transit gateway.

To create an unbound GRE tunnel, follow these steps:

1. Select one of the following choices:

   * To create an unbound GRE tunnel on an existing transit gateway:
      1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
      1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**.
      1. Click the name of the transit gateway where you want to add a connection.
      1. Click **Add connection** in the Connections tab.

   * To create an unbound GRE tunnel while creating a transit gateway:
      1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
      1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**.
      1. Click **Create transit gateway** to open the provisioning page.
      1. Enter the transit gateway name, resource group, and location.

1. Choose **Unbound GRE tunnel** as your network connection type.
1. Enter the tunnel name.
1. Select the base network type and whether this is a connection to a network in another account.
1. If this connection is to a network in another account, enter the account ID.
1. Choose an availability zone in which to create the tunnel.
1. Configure the remaining parameters for the connection:
   * Enter the remote gateway IP for the endpoint of the GRE tunnel.
   * Enter a `/30` remote tunnel IP for both ends of the tunnel, for example `192.168.103.2`.
   * Enter the local gateway IP address[^ip1] that the transit gateway uses to host the underlay network for the GRE tunnel. This user-selected IP address is configured on the transit gateway GRE tunnel after the tunnel is created.
   * Enter a `/30` local tunnel IP for both ends of the tunnel, for example `192.168.103.1`.
   * Optionally, enter the remote BGP ASN, which is a valid 2 or 4 byte value of your choosing.

      You can leave this blank and a unique ASN is assigned.
      {: tip}

   * Enter a connection name for your GRE tunnel.
1. Click **Add** to create the GRE tunnel.

### Next steps
{: #tgw-next-step-unbound-gre}

To configure the other end of the BGP tunnel, expand the newly created unbound GRE tunnel in the Connections panel to see its details. It will show the Local BGP ASN. If you created an optional remote BGP ASN, it also shows in the Connections panel. You must give this ASN information to the person creating the other end of the BGP tunnel, so that the BGP session can be fully configured.

[^ip1]: This IP address must not be an IP address within the multicast range of `224.0.0.0` to `239.255.255.255` and cannot be in conflict with any existing networks connected to the transit gateway.

## Creating an unbound GRE tunnel from the CLI
{: #tg-cli-adding-unbound-gre-connection-transit-gateway}
{: cli}

Create an unbound Generic Routing Encapsulation (GRE) tunnel connection on a given transit gateway.

```sh
ibmcloud tg connection-create-gre|ccgre GATEWAY_ID --name NAME --zone ZONE --local-gateway-ip LOCAL_GATEWAY_IP --local-tunnel-ip LOCAL_TUNNEL_IP --remote-gateway-ip REMOTE_GATEWAY_IP --remote-tunnel-ip REMOTE_TUNNEL_IP [--network-type NETWORK_TYPE] [--base-connection-id BASE_CONNECTION_ID] [--base-network-type BASE_NETWORK_TYPE] [--network-account-id NETWORK_ACCOUNT_ID] [--remote-bgp-asn REMOTE_BGP_ASN] [--output json]
```
{: pre}

Where:

**GATEWAY_ID**
:   ID of the gateway where the new connection is bound.

**--name**
:   Name of the new connection.

**--zone**
:   Availability zone for the GRE tunnel. Example: `us-south-1`

**--local-gateway-ip**
:   Local gateway IP address for the GRE tunnel connection.

**--local-tunnel-ip**
:   Local tunnel IP address for the GRE tunnel connection.

**--remote-gateway-ip**
:   Remote gateway IP address for the GRE tunnel connection.

**--local-tunnel-ip**
:   Remote tunnel IP address for the GRE tunnel connection.

**--network-type**
:   Optional: The type of GRE tunnel to create, either `gre_tunnel` or `unbound_gre_tunnel`. The default is `gre_tunnel`.

**--base-connection-id**
:   Optional: The ID of the classic network connection that will be the underlay for the GRE tunnel. Used only for `gre_tunnel` type connections.

**--base-network-type**
:   Optional: The type of network the GRE tunnel is targeting (classic). Used only for `unbound_gre_tunnel` type connections.

**--network-account-id**
:   Optional: The ID of the IBM Cloud account to use for creating a cross account GRE tunnel to a classic network. Used only for `unbound_gre_tunnel` type connections.

**--remote-bgp-asn**
:   Optional: If the remote BGP ASN is not specified, one is generated.

**--output json**
:   Optional: Shows the output in JSON format.

**--help | -h**
:   Optional: Get help on this command.

### Example
{: #connection-create-unbound-gre-examples}

This example illustrates creating an unbound GRE tunnel named `unbound-gre-connection` to a classic network:

```sh
ibmcloud tg connection-create-gre $gateway  --network-type unbound_gre_tunnel --name unbound-gre-connection --base-network-type classic  --zone us-south-2 --local-gateway-ip 192.168.100.1 --local-tunnel-ip 192.168.101.1 --remote-gateway-ip 10.242.63.12 --remote-tunnel-ip 192.168.101.2
```
{: pre}

## Creating an unbound GRE tunnel with the API
{: #tg-api-adding-unbound-gre-connection-transit-gateway}
{: api}

### Example Request
{: #add-unbound-gre-connection-curl-api-request-example}

This example illustrates requesting a GRE connection:

```sh
curl -X POST "https://transit.cloud.ibm.com/v1/transit_gateways/test/connections?version=2022-01-27" -H "accept: application/json" -H "Content-Type: application/json" -d "{\"local_gateway_ip\":\"192.168.100.1\",\"local_tunnel_ip\":\"192.168.129.2\",\"name\":\"Transit_Service_BWTN_SJ_DL\",\"network_type\":\"unbound_gre_tunnel\",\"base_network_type\":\"classic\",\"remote_bgp_asn\":65010,\"remote_gateway_ip\":\"10.242.63.12\",\"remote_tunnel_ip\":\"192.168.129.1\",\"zone\":{\"name\":\"us-south-1\"}}"
```
{: pre}

The payload for this request is as follows:

```json
{
  "local_gateway_ip": "192.168.100.1",
  "local_tunnel_ip": "192.168.129.2",
  "name": "Transit_Service_BWTN_SJ_DL",
  "network_type": "unbound_gre_tunnel",
  "base_network_type": "classic",
  "remote_bgp_asn": 65010,
  "remote_gateway_ip": "10.242.63.12",
  "remote_tunnel_ip": "192.168.129.1",
  "zone": {
    "name": "us-south-1"
  }
}
```
{: pre}

### Example Response
{: #add-unbound-gre-connection-curl-api-response-example}

This example illustrates the response from creating an unbound GRE tunnel:

```json
{
  "created_at": "2020-03-31T12:08:05Z",
  "id": "1a15dca5-7e33-45e1-b7c5-bc690e569531",
  "name": "example-connection",
  "network_type": "unbound_gre_tunnel",
  "base_network_type": "classic",
  "status": "pending",
  "updated_at": "2020-03-31T12:08:05Z"
}
```
{: screen}

For more information, see [Adds a connection to a Transit Gateway](/apidocs/transit-gateway#create-transit-gateway-connection) in the Transit Gateway API reference.
{: note}

## Creating a GRE tunnel connection using Terraform
{: #tg-terraform-adding-unbound-gre-connection-transit-gateway}
{: terraform}

You can specify the following argument references for your resource when creating an unbound Generic Routing Encapsulation (GRE) tunnel connection:

|Argument|Details|
|--|--|
|**gateway**  \n Required  \n Forces new resource  \n string|Enter the transit gateway identifier.|
|**local_gateway_ip**  \n Optional  \n Forces new resource  \n string | The local gateway IP address.  \n This field is required for, and only applicable to, `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**local_tunnel_ip**  \n Optional  \n Forces new resource  \n string|The local tunnel IP address.  \n This field is required for, and only applicable to, `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**name**  \n Optional  \n string | The name of the connection. If the name is not given, the default name is provided based on the network type, such as `unbound_gre_tunnel` for network type unbound gre.|
|**network_type**  \n Required  \n Forces new resource  \n string | The network type. Allowed values are `gre_tunnel` and `unbound_gre_tunnel`.
|**base_network_type**  \n Optional  \n Forces new resource  \n string| The base network type. Allowed values are `classic`.  \n This field only applies to `unbound_gre_tunnel` type connections.
|**remote_bgp_asn**  \n Optional  \n Forces new resource  \n integer | The remote network BGP ASN. It will be generated for the connection if not specified.  \n This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**remote_gateway_ip**  \n Optional  \n Forces new resource  \n string | The remote gateway IP address. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**remote_tunnel_ip**  \n Optional  \n Forces new resource  \n string | The remote tunnel IP address. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**zone**  \n Optional  \n Forces new resource  \n string | The location of the GRE tunnel. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
{: caption="Terraform argument references for creating a GRE" caption-side="bottom"}

### Example
{: #tg-terraform-adding-unbound-gre-connection-transit-gateway-example}

This example illustrates requesting an unbound GRE tunnel:

```sh
resource "ibm_tg_connection" "test_ibm_tg_connection" {
  gateway            = ibm_tg_gateway.test_tg_gateway.id
  network_type       = "unbound_gre_tunnel"
  base_network_type  = "classic"
  name               = "myconnection"
  local_gateway_ip   = 192.168.0.1
  local_tunnel_ip    = 10.0.0.1
  remote_bgp_asn     = 36361
  remote_gateway_ip  = 192.168.1.1
  remote_tunnel_ip   = 10.0.1.1
  zone               = us-east
}
```
{: pre}
