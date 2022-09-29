---

copyright:
  years: 2020, 2022
lastupdated: "2022-08-31"

keywords: editing, managing, manage, edit, add, connection

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Creating a Generic Routing Encapsulation (GRE) tunnel connection
{: #GRE-connection}

## Creating a Generic Routing Encapsulation (GRE) tunnel connection using the UI
{: #tg-ui-adding-gre-connection-transit-gateway}
{: ui}

You can use a GRE tunnel transit gateway connection to connect endpoints. This connection allows a transit gateway to connect to overlay networks hosted on classic infrastructure resources.
{: shortdesc}

Transit gateway GRE connections require the gateway owner to specifically configure HA for their needs. A GRE connection is a point to point connection, has no built in redundancy, and is a single point of failure. When configuring a GRE connection on a transit gateway, you must specify the availability zone. For a robust HA solution, configure multiple GRE connections using different availability zones.
{: note}

### Before you begin
{: #GRE-begin}

The following prerequisites must be met before you can create a GRE tunnel connection:

* Ensure that you have an existing classic infrastructure connection, or create one. For more information, see [Adding a connection](/docs/transit-gateway?topic=transit-gateway-adding-connections). The GRE tunnel connection connects with an endpoint only on classic infrastructure.
* Review the [Generic Routing Encapsulation (GRE) connection considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#gre-considerations) for additional prerequisites.

### Creating a GRE tunnel connection
{: #creating-gre}

To create your GRE tunnel connection, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com){: external} and log in to your account.
1. Select the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Interconnectivity**.
1. Click **Transit Gateway** from the left navigation panel. Click the name of the transit gateway where you want to add a connection.

   If you are in the expanded view, click **View details**.
   {: tip}

1. Click **Add connection**.
1. Choose **GRE tunnel** as your network connection type.
1. Choose an availability zone in which to create the tunnel, then select the base connection (which must be a classic infrastructure connection).
1. Configure the remaining parameters for the connection:
   * Enter the remote gateway IP[^ip1] for the endpoint of the GRE tunnel.
   * Enter a `/30` remote tunnel IP[^ip2] for both ends of the tunnel, for example `192.168.103.2`.
   * Enter the local gateway IP address that the transit gateway uses to host the underlay network for the GRE tunnel. This user-selected IP address is configured on the Transit Gateway GRE tunnel after the tunnel is created.

      This IP address must not conflict with any networks connected to your transit gateway.
      {: note}

   * Enter a `/30` local tunnel IP[^ip3] for both ends of the tunnel, for example `192.168.103.1`.
   * Optionally, enter the remote BGP ASN, which is a valid 2 or 4 byte value of your choosing.

      You can leave this blank and a unique ASN is assigned.
      {: tip}
      
   * Enter a connection name for your GRE tunnel.

1. Click the **Add** button to create the GRE tunnel.

   ![Create GRE tunnel connections](images/GreTunnelConnection.png "Creating GRE connection"){: caption="Creating GRE tunnel connections" caption-side="bottom"}

### Next step
{: #tgw-next-step-gre}

To configure the other end of the BGP tunnel, expand the newly created GRE tunnel in the Connections panel to see its details. It will show the Local BGP ASN. If you created an optional remote BGP ASN, it also shows in the Connections panel. You must give this ASN information to the person creating the other end of the BGP tunnel, so that the BGP session can be fully configured.

[^ip1]: This address must comply with rfc1918 IP addresses and cannot be in conflict with any existing networks connected to the transit gateway.

[^ip2]: This address must comply with rfc1918 IP addresses and cannot be in conflict with any existing networks connected to the transit gateway.

[^ip3]: This address must comply with rfc1918 IP addresses and cannot be in conflict with any existing networks connected to the transit gateway.

## Creating a Generic Routing Encapsulation (GRE) tunnel connection using the CLI
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

- **--zone**: Availability zone for the GRE tunnel. Example: 'us-south-1'

- **--base-connection-id**: ID of the classic network connection that will be the underlay for the GRE tunnel.

- **--local-gateway-ip**: Local gateway IP address for the GRE tunnel connection.

- **--local-tunnel-ip**: Local tunnel IP address for the GRE tunnel connection.

- **--remote-gateway-ip**: Remote gateway IP address for the GRE tunnel connection.

- **--local-tunnel-ip**: Remote tunnel IP address for the GRE tunnel connection.

- **--remote-bgp-asn**: Optional: If the remote BGP ASN is not specified, one is generated.

- **--output json**: Optional: Shows the output in JSON format.

- **--help | -h**: Optional: Get help on this command.

### Example
{: #connection-create-gre-examples}

Create a GRE tunnel connection named `gre-connection` using classic connection `9037f710-8dfb-4948-a2bd-847c8dde96d3` as the base connection:

```sh
ibmcloud tg connection-create-gre $gateway  --name gre-connection --base-connection-id 9037f710-8dfb-9999-a2bd-847c8dde96d3  --zone us-south-2 --local-gateway-ip 192.168.100.1 --local-tunnel-ip 192.168.101.1 --remote-gateway-ip 10.242.63.12 --remote-tunnel-ip 192.168.101.2
```
{: pre}

## Creating a Generic Routing Encapsulation (GRE) tunnel connection using the API
{: #tg-api-adding-gre-connection-transit-gateway}
{: api}

To create a Generic Routing Encapsulation (GRE) tunnel connection using the API, perform the following actions:

### Request
{: #add-gre-connection-curl-api-request}

To request a creation of a Generic Routing Encapsulation (GRE) tunnel connection, set the following parameters:

| Path parameters | Details |
|--|--|
|**transit_gateway_id**  \n Required  \n string | The transit gateway identifier|
{: caption="Table 1. Path parameters for creating a GRE" caption-side="bottom"}

|Query parameters| Details |
|--|--|
|**version**  \n Required  \n string | Requests the version of the API as of a date in the format `YYYY-MM-DD`. Any date up to the current date may be provided. Specify the current date to request the latest version.  \n **Possible values:** Value must match regular expression  `^[0-9]{4}-[0-9]{2}-[0-9]{2}$`|
|**Request Body**  \n Required  \n TransitGatewayConnectionTemplate | The connection template|
|**network_type**  \n Required  \n string | Defines what type of network is connected via this connection.  \n For access to gre_tunnel connections contact IBM support.  \n **Allowable value:** [`gre_tunnel`]  \n **Example:** `gre_tunnel`|
|**base_connection_id**  \n string|network_type 'gre_tunnel' connections must be created over an existing network_type 'classic' connection. This field is required for 'gre_tunnel' connections and must specify the ID of an active transit gateway network_type 'classic' connection in the same transit gateway. Omit 'base_connection_id' for any connection type other than 'gre_tunnel'.  \n **Example:** `975f58c1-afe7-469a-9727-7f3d720f2d32`|
|**local_gateway_ip**  \n string | Local gateway IP address. This field is required for and only applicable to type gre_tunnel connections.  \n **Example:** `192.168.100.1`|
|**local_tunnel_ip**  \n string|Local tunnel IP address. This field is required for and only applicable to type 'gre_tunnel' connections. The 'local_tunnel_ip' and 'remote_tunnel_ip' addresses must be in the same /30 network. Neither can be the network nor broadcast addresses.  \n **Example:** `192.168.129.2`|
|**name**  \n Name|The user-defined name for this transit gateway connection.  \n Name specification is required for network type 'gre_tunnel' connections.  \n **Possible values:** 1 ≤ length ≤ 63, Value must match regular expression ^([a-zA-Z]|[a-zA-Z][-_a-zA-Z0-9]*[a-zA-Z0-9])$  \n **Example:** `Transit_Service_BWTN_SJ_DL`|
|**remote_bgp_asn**  \n string|Remote network BGP ASN. This field is only applicable to 'gre_tunnel' type connections. The following ASN values are reserved and unavailable 64512-64513, 65100, 65201-65234, 65402-65433, 65500 and 4201065000-4201065999. If 'remote_bgp_asn' is omitted on gre_tunnel connection create requests IBM will assign an ASN.  \n **Example:** `65010`|
|**remote_gateway_ip**  \n string|Remote gateway IP address. This field is required for and only applicable to type gre_tunnel connections.  \n **Example:** `10.242.63.12`|
|**remote_tunnel_ip**  \n string|Remote tunnel IP address. This field is required for and only applicable to type gre_tunnel connections. The local_tunnel_ip and remote_tunnel_ip addresses must be in the same /30 network. Neither can be the network nor broadcast addresses.  \n **Example:** `192.168.129.1`|
|**zone**  \n ZoneIdentityByName|For network_type 'gre_tunnel' connections specify the connection's location. The specified availability zone must reside in the gateway's region. Use the IBM Cloud global catalog to list zones within the desired region. This field is required for and only applicable to network type 'gre_tunnel' connections.|
|- **name**  \n string|Availability zone name.  \n **Example:** `us-south-1`|
{: caption="Table 2. Query parameters for creating a GRE" caption-side="bottom"}

#### Example request
{: #add-gre-connection-curl-api-request-example}

This example illustrates requesting a GRE connection:

```sh
curl -X POST "https://transit.cloud.ibm.com/v1/transit_gateways/test/connections?version=2022-01-27" -H "accept: application/json" -H "Content-Type: application/json" -d "{\"base_connection_id\":\"975f58c1-afe7-469a-9727-7f3d720f2d32\",\"local_gateway_ip\":\"192.168.100.1\",\"local_tunnel_ip\":\"192.168.129.2\",\"name\":\"Transit_Service_BWTN_SJ_DL\",\"network_type\":\"gre_tunnel\",\"prefix_filters\":[{\"action\":\"permit\",\"ge\":0,\"le\":32,\"prefix\":\"192.168.100.0/24\"}],\"prefix_filters_default\":\"permit\",\"remote_bgp_asn\":65010,\"remote_gateway_ip\":\"10.242.63.12\",\"remote_tunnel_ip\":\"192.168.129.1\"}"

{
  "base_connection_id": "975f58c1-afe7-469a-9727-7f3d720f2d32",
  "local_gateway_ip": "192.168.100.1",
  "local_tunnel_ip": "192.168.129.2",
  "name": "Transit_Service_BWTN_SJ_DL",
  "network_type": "gre_tunnel",
  "prefix_filters": [
    {
      "action": "permit",
      "ge": 0,
      "le": 32,
      "prefix": "192.168.100.0/24"
    }
  ],
  "prefix_filters_default": "permit",
  "remote_bgp_asn": 65010,
  "remote_gateway_ip": "10.242.63.12",
  "remote_tunnel_ip": "192.168.129.1"
}
```
{: pre}

### Response
{: #add-gre-connection-curl-api-response}

The following response results show once you initiate the request:

| Response body | Details |
|--|--|
|**name**  \n Always included*  \n Name|The user-defined name for this transit gateway connection.  \n **Possible values:** 1 ≤ length ≤ 63, Value must match regular expression  `^([a-zA-Z]|[a-zA-Z][-_a-zA-Z0-9]*[a-zA-Z0-9])$`  \n **Example:** `Transit_Service_BWTN_SJ_DL`|
|**network_type**  \n Always included*  \n string|Defines what type of network is connected via this connection. The list of enumerated values for this property may expand in the future. Code and processes using this field must tolerate unexpected values.  \n **Possible values:** [`gre_tunnel`]  \n **Example:** `gre-tunnel`|
|**id**  \n Always included*  \n string | The unique identifier for this Transit Gateway Connection  \n **Example:** `1a15dca5-7e33-45e1-b7c5-bc690e569531`|
|**created_at** \n Always included*  \n date-time|The date and time that this connection was created|
|**base_connection_id**  \n string|network_type 'gre_tunnel' connections use 'base_connection_id' to specify the ID of a network_type 'classic' connection the tunnel is configured over. The specified connection must reside in the same transit gateway and be in an active state. The 'classic' connection cannot be deleted until any 'gre_tunnel' connections using it are deleted. This field only applies to and is required for network type 'gre_tunnel' connections.  \n **Example:** `975f58c1-afe7-469a-9727-7f3d720f2d32`|
|**local_bgp_asn**  \n integer|Local network BGP ASN. This field only applies to network type 'gre_tunnel' connections.  \n **Example:** `64490`|
|**local_gateway_ip**  \n string| Local gateway IP address. This field only applies to network type 'gre_tunnel' connections.  \n **Example:** `192.168.100.1`|
|**local_tunnel_ip** \n string|Local tunnel IP address. This field only applies to network type 'gre_tunnel' connections.  \n **Example:** `192.168.129.2`|
|**mtu**  \n integer|GRE tunnel MTU. This field only applies to network type 'gre_tunnel' connections.  \n **Example:** `9000`|
|**remote_bgp_asn**  \n integer | Remote network BGP ASN. This field only applies to network type 'gre_tunnel' connections.  \n **Example:** `65010`|
|**remote_gateway_ip**  \n string|Remote gateway IP address. This field only applies to network type 'gre_tunnel' connections.  \n **Example:** `10.242.63.12`|
|**remote_tunnel_ip**  \n string|Remote tunnel IP address. This field only applies to network type 'gre_tunnel' connections.  \n **Example:** `192.168.129.1`|
|**request_status**  \n string|Only visible for cross account connections, this field represents the status of a connection request between IBM Cloud accounts. The list of enumerated values for this property may expand in the future. Code and processes using this field must tolerate unexpected values.  \n **Possible values:** [`pending`,`approved`,`rejected`,`expired`,`detached`]|
|**status**  \n string|Connection's current configuration state. The list of enumerated values for this property may expand in the future. Code and processes using this field must tolerate unexpected values.  \n **Possible values:** [`attached`,`failed`,`pending`,`deleting`,`detaching`,`detached`]|
|**updated_at**  \n date-time|The date and time that this connection was last updated|
|**zone**  \n ZoneReference|Location of GRE tunnel. This field only applies to network type 'gre_tunnel' connections.|
|- **name**  \n Always included*  \n string|Availability zone name  \n **Example:** `us-south-1`|
{: caption="Table 3. Initating request response" caption-side="bottom"}

|Status Code||
|--|--|
|**201**|The Transit Gateway connection was created successfully.|
|**400**|An invalid connection template was provided.|
|**404**|The specified Transit Gateway could not be found, the specified resource group could not be found, or the default resource group could not be found (if the resource group was not specified in the template).|
|**409**|The network being connected must either be in a location that is considered "local" to the specified Transit Gateway, or the specified Transit Gateway needs to be global. The network being connected cannot already be connected to another Transit Gateway.|
{: caption="Table 4. Status codes" caption-side="bottom"}

#### Example response
{: #add-gre-connection-curl-api-response-example}

This example illustrates the response from creating a GRE tunnel:

```sh
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

For more information (including Java, Node, Python and Go examples), see "Add Connection to a Transit Gateway" in the [Transit Gateway API reference](apidocs/transit-gateway?code=java#create-transit-gateway-connection).
{: note}

## Creating a Generic Routing Encapsulation (GRE) tunnel connection using Terraform
{: #tg-terraform-adding-gre-connection-transit-gateway}
{: terraform}

You can specify the following argument references for your resource when creating a Generic Routing Encapsulation (GRE) tunnel connection:

|Argument|Details|
|--|--|
|**base_connection_id**  \n Optional  \n Forces new resource  \n string|The ID of a network_type 'classic' connection a tunnel is configured over.  \n This field only applies to network type `gre_tunnel` connections.|
|**gateway**  \n Required  \n Forces new resource  \n string|Enter the transit gateway identifier.|
|**local_gateway_ip**  \n Optional  \n Forces new resource  \n string|The local gateway IP address.  \n This field is required for and only applicable to `gre_tunnel` connection types.|
|**local_tunnel_ip**  \n Optional  \n Forces new resource  \n string|The local tunnel IP address.  \n This field is required for and only applicable to type `gre_tunnel` connections.|
|**name**  \n Optional  \n string|Enter a name. If the name is not given, the default name is provided based on the network type, such as `gre_tunnel` for network type gre.|
|**network_type**  \n Required  \n Forces new resource  \n string|Enter the network type. Allowed values are `gre_tunnel`
|**remote_bgp_asn**  \n Optional  \n Forces new resource  \n integer|The remote network BGP ASN (will be generated for the connection if not specified).  \n This field only applies to network type `gre_tunnel` connections.|
|**remote_gateway_ip**  \n Optional  \n Forces new resource  \n string|The remote gateway IP address. This field only applies to network type `gre_tunnel` connections.|
|**remote_tunnel_ip**  \n Optional  \n Forces new resource  \n string|The remote tunnel IP address. This field only applies to network type `gre_tunnel` connections.|
|**zone**  \n Optional  \n Forces new resource  \n string|The location of the GRE tunnel. This field only applies to network type `gre_tunnel` connections.|
{: caption="Table 5. Terraform argument references for creating a GRE" caption-side="bottom"}

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
