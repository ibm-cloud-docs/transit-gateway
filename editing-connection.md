---

copyright:
  years: 2020, 2022
lastupdated: "2022-02-18"

keywords: editing, managing, manage, edit, add, connection

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Editing a connection
{: #editing-connections}

## Editing a connection in the UI
{: #editing-connections-ui}
{: ui}

To edit a connection to a transit gateway, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Interconnectivity**.
1. Click **Transit Gateway** from the left navigation pane.
1. Click the name of the transit gateway where you want to edit a connection.

   If you are in the expanded view, click **View details**.
   {: tip}

1. From the Connections page, click the Actions menu ![Actions menu](/images/overflow.png) next to the connection that you want to edit and select **Edit**.

   From here, you can change the name of the selected network connection.
   
## Editing a connection from the CLI
{: #editing-connections-cli}
{: cli}

To edit a connection from the CLI, execute this command:

```sh
ibmcloud tg connection-update|cu GATEWAY_ID CONNECTION_ID --name NAME [--output json] [-h, --help]
```
{: pre}

Where:

- **GATEWAY_ID**: ID of the gateway the connection being updated is on.

- **CONNECTION_ID**: ID of the connection to update.

- **--name**: New name of the connection.

- **--output json**: Optional: Specify if you want the output displayed in JSON format.

- **--help | -h**: Optional: Get help on this command.

### Example
{: #editing-connections-cli-example}

This example illustrates updating the name of a connection to `MyConn2`:

```sh
ibmcloud tg cu $gateway $connection --name MyConn2
```
{: pre}

## Editing a connection with the API
{: #editing-connections-api}
{: api}

You can update the name of a connection for a transit gateway with the API.

### Request 
{: #editing-connections-api-request}

To edit a connection, set the following parameters:

|Path parameters|Details|
|--|--|
|**transit_gateway_id**  \n Required  \n string|The Transit Gateway identifier|
|**id**  \n Required  \n string|The connection identifier|
{: caption="Table 1. Path parameters for editing a connection" caption-side="bottom"}

|Query parameters|Details|
|--|--|
|**version**  \n Required  \n string|Requests the version of the API as of a date in the format `YYYY-MM-DD`. Any date up to the current date may be provided. Specify the current date to request the latest version.  \n **Possible values:** Value must match regular expression  `^[0-9]{4}-[0-9]{2}-[0-9]{2}$`|
|**Request Body**  \n Required  \n TransitGatewayConnectionActions | The action template|
|**name**  \n Name|The user-defined name for this transit gateway connection.  \n Name specification is required for network type `gre_tunnel` and `unbound_gre_tunnel` connections.  \n **Possible values:** 1 ≤ length ≤ 63, Value must match regular expression ^([a-zA-Z]|[a-zA-Z][-_a-zA-Z0-9]*[a-zA-Z0-9])$  \n **Example:** `Transit_Service_BWTN_SJ_DL`|
{: caption="Table 2. Query parameters for editing a connection" caption-side="bottom"}

#### Example Request
 {: #editing-connections-api-request-example}

This example illustrates editing the name of a transit gateway connection:

 
```sh
PATCH 
/transit_gateways/{transit_gateway_id}/connections/{id}
{  
  "name":  "Transit_Service_BWTN_SJ_DL",  
  "prefix_filters_default":  "permit"  
}
```
{: pre}

### Response
{: #editing-connections-api-response}

The following response shows after you initiate the request:

| Response body |Details|
|--|--|
|**name**  \n Always included  \n Name|The user-defined name for this transit gateway connection.  \n **Possible values:** 1 ≤ length ≤ 63, Value must match regular expression  `^([a-zA-Z]|[a-zA-Z][-_a-zA-Z0-9]*[a-zA-Z0-9])$`  \n **Example:** `Transit_Service_BWTN_SJ_DL`|
|**network_type**  \n Always included  \n string|Defines what type of network is connected via this connection. The list of enumerated values for this property may expand in the future. Code and processes using this field must tolerate unexpected values.  \n **Possible values:** [`classic`,`directlink`,`gre_tunnel`,`unbound_gre_tunnel`,`vpc`]  \n **Example:** `vpc`|
|**id**  \n Always included  \n string | The unique identifier for this Transit Gateway Connection  \n **Example:** `1a15dca5-7e33-45e1-b7c5-bc690e569531`|
|**created_at** \n Always included  \n date-time|The date and time that this connection was created|
|**base_network_type**  \n string|Defines the type of network the GRE tunnel targets. This field only applies to `unbound_gre_tunnel` type connections. The list of enumerated values for this property may expand in the future. Code and processes using this field must tolerate unexpected values.
|**network_id**  \n string|The ID of the network being connected to using this connection. This field is required for some types, such as `vpc` and `directlink` For network types `vpc` and `directlink` it should be the CRN of the target vpc / gateway respectively.  \n **Example:** `crn:v1:bluemix:public:is:us-south:a/123456::vpc:4727d842-f94f-4a2d-824a-9bc9b02c523b`|
|**base_connection_id**  \n string|network_type `gre_tunnel` connections use `base_connection_id` to specify the ID of a network_type `classic` connection the tunnel is configured over. The specified connection must reside in the same transit gateway and be in an active state. The `classic` connection cannot be deleted until any `gre_tunnel` connections using it are deleted. This field only applies to and is required for network type `gre_tunnel` connections.  \n **Example:** `975f58c1-afe7-469a-9727-7f3d720f2d32`|
|**local_bgp_asn**  \n integer|The local network BGP ASN. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.  \n **Example:** `64490`|
|**local_gateway_ip**  \n string| The local gateway IP address. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.  \n **Example:** `192.168.100.1`|
|**local_tunnel_ip** \n string|The local tunnel IP address. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.  \n **Example:** `192.168.129.2`|
|**mtu**  \n integer|The GRE tunnel MTU. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.  \n **Example:** `9000`|
|**network_account_id**  \n AccountID|The ID of the account which owns the connected network. Generally only used if the network is in a different IBM Cloud account than the gateway.  \n **Example:** `28e4d90ac7504be694471ee66e70d0d5`|
|**remote_bgp_asn**  \n integer | The remote network BGP ASN. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.  \n **Example:** `65010`|
|**remote_gateway_ip**  \n string|The remote gateway IP address. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.  \n **Example:** `10.242.63.12`|
|**remote_tunnel_ip**  \n string|Remote tunnel IP address. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.  \n **Example:** `192.168.129.1`|
|**request_status**  \n string|Only visible for cross account connections, this field represents the status of a connection request between IBM Cloud accounts. The list of enumerated values for this property may expand in the future. Code and processes using this field must tolerate unexpected values.  \n **Possible values:** [`pending`,`approved`,`rejected`,`expired`,`detached`]|
|**status**  \n string|Connection's current configuration state. The list of enumerated values for this property may expand in the future. Code and processes using this field must tolerate unexpected values.  \n **Possible values:** [`attached`,`failed`,`pending`,`deleting`,`detaching`,`detached`]|
|**updated_at**  \n date-time|The date and time that this connection was last updated|
|**zone**  \n ZoneReference|The location of the GRE tunnel. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|- **name**  \n Always included  \n string|Availability zone name  \n **Example:** `us-south-1`|
{: caption="Table 3. Initiation request" caption-side="bottom"}

|Status Code||
|--|--|
|**200**|The connection was updated successfully.|
|**400**|The connection update template was invalid.|
|**404**|A connection or gateway with the specified identifier(s) could not be found.|
{: caption="Table 4. Status codes" caption-side="bottom"}

#### Example Response
{: #editing-connections-api-response-example}

The following response indicates that the connection was updated successfully:

```sh
{
  "name": "Transit_Service_BWTN_SJ_DL",
  "network_id": "crn:v1:bluemix:public:is:us-south:a/123456::vpc:4727d842-f94f-4a2d-824a-9bc9b02c523b",
  "network_type": "vpc",
  "id": "1a15dca5-7e33-45e1-b7c5-bc690e569531",
  "base_connection_id": "975f58c1-afe7-469a-9727-7f3d720f2d32",
  "created_at": "2022-02-10T14:52:54.918Z",
  "local_bgp_asn": 64490,
  "local_gateway_ip": "192.168.100.1",
  "local_tunnel_ip": "192.168.129.2",
  "mtu": 9000,
  "network_account_id": "28e4d90ac7504be694471ee66e70d0d5",
  "prefix_filters": [
    {
      "action": "permit",
      "before": "1a15dcab-7e40-45e1-b7c5-bc690eaa9782",
      "created_at": "2022-02-10T14:52:54.918Z",
      "ge": 0,
      "id": "1a15dcab-7e30-45e1-b7c5-bc690eaa9865",
      "le": 32,
      "prefix": "192.168.100.0/24",
      "updated_at": "2022-02-10T14:52:54.918Z"
    }
  ],
  "prefix_filters_default": "permit",
  "remote_bgp_asn": 65010,
  "remote_gateway_ip": "10.242.63.12",
  "remote_tunnel_ip": "192.168.129.1",
  "request_status": "pending",
  "status": "attached",
  "updated_at": "2022-02-10T14:52:54.918Z",
  "zone": {
    "name": "us-south-1"
  }
}
```
{: screen}

For more information (including Java, Node, Python and Go examples), see "Update Specified Transit Gateway Connection" in the [Transit Gateway API reference](/apidocs/transit-gateway#update-transit-gateway-connection).
{: note}

## Editing a connection using terraform
{: #editing-connections-terraform}
{: terraform}

You can specify the following argument references for your resource when editing a transit gateway connection:

|Argument|Details|
|--|--|
|**gateway**  \n Required  \n String | Enter the transit gateway identifier.|
|**network_type**  \n Required  \n String|Enter the network type. Allowed values are `classic, directlink, gre_tunnel, unbound_gre_tunnel, and vpc`|
|**name**  \n Optional  \n String | Enter a name. If the name is not given, the default name is provided based on the network type, such as `vpc` for network type VPC and `classic` for network type classic.|
{: caption="Table 5. Terraform argument references for editing a connection" caption-side="bottom"}

### Example
{: #change-configuration-terraform-example}

This example illustrates editing a transit gateway connection in Terraform:

```sh
resource "ibm_tg_connection" "test_ibm_tg_connection" {
  gateway      = ibm_tg_gateway.test_tg_gateway.id
  network_type = "vpc"
  name         = "myconnection"
}
```
{: pre}
