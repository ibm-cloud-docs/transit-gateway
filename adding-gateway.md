---

copyright:
  years: 2020, 2023
lastupdated: "2023-10-09"

keywords: features, overview

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Adding a connection
{: #adding-connections}

You can add a connection to a transit gateway using the UI, CLI, and API.
{: shortdesc}

## Adding a connection in the UI
{: #tg-ui-adding-connection-transit-gateway}
{: ui}

To add a connection to a transit gateway, follow these steps:
1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Interconnectivity**.
1. Click **Transit Gateway** from the left navigation pane.
1. Click the name of the transit gateway where you want to add a connection.

   If you are in the expanded view, click **View details**.
   {: tip}

1. Click **Add connection**.

1. Choose and configure the specific network connections that you want to add to your transit gateway. Choices include:

   * **Classic infrastructure** - Allows you to connect to IBM Cloud classic resources.
   * **VPC** - Allows you to connect to your account's VPC resources, or VPC resources from other accounts as well.
   * **Unbound GRE tunnel** - Allows a transit gateway to connect to overlay networks hosted on classic infrastructure resources. For prerequisites and detailed instructions, see [Creating an Unbound Generic Routing Encapsulation tunnel connection](/docs/transit-gateway?topic=transit-gateway-unbound-gre-connection).
   * **Direct Link** - Creates a network connection to and from Direct Link gateways so that there is a secure connection to on-premises networks and other resources connected to the transit gateway.

      If you select **Direct Link**, you must also log in to the [Direct Link console](https://cloud.ibm.com/interconnectivity/direct-link){: external} (using the same IBM Cloud account) and specify **Transit Gateway** as the type of network connection for your direct link.
      {: important}

   * **{{site.data.keyword.powerSys_notm}}** - Creates a network connection to and from a {{site.data.keyword.powerSys_notm}} instance so that there is a secure connection to networks and other resources connected to the transit gateway.

      Location: Select a region for the {{site.data.keyword.powerSys_notm}} workspace.

      If you select **{{site.data.keyword.powerSys_notm}}**, you must have a {{site.data.keyword.powerSys_notm}} workspace created in a data center after the Power Edge Router has been deployed. To find out if your {{site.data.keyword.powerSys_notm}} workspace is set up correctly, go to the workspace and check the navigation for a Cloud connections page. If there isn't a **Cloud connections** page, the workspace leverages the Power Edge Router and can be added as a connection to Transit Gateway. Otherwise, you must configure virtual connections with Cloud connections on the {{site.data.keyword.powerSys_notm}}.
      {: important}

1. Click **Add** to create a connection.

## Adding a connection from the CLI
{: #tg-cli-adding-connection-transit-gateway}
{: cli}

### Before you begin
{: #cli-prereqs-before-you-begin}

Complete these prerequisites to use the Transit Gateway CLI, which is implemented as an {{site.data.keyword.cloud_notm}} CLI plug-in.

1. Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli#install-ibmcloud-cli){: external}.
1. Install the `tg-cli/tg` CLI plug-in to the {{site.data.keyword.cloud_notm}} CLI.

   To install:

   ```sh
   ibmcloud plugin install tg
   ```
   {: pre}

If you are going to use the CLI with a Virtual Private Endpoint (VPE), you must set the following variable:

```bash
export IBMCLOUD_TG_API_ENDPOINT=private.transit.cloud.ibm.com
```
{: pre}

For more information, see [Integrating with Virtual Private Endpoint for VPC](/docs/transit-gateway?topic=transit-gateway-vpe-for-ibm-cloud-transit-gateway).
{: note}

To add a connection on the transit gateway from the CLI, enter the following command:

```sh
ibmcloud tg connection-create|cc GATEWAY_ID --name NAME --network-type [vpc | directlink | classic] --network-id NETWORK_ID --network-account-id NETWORK-ACCOUNT-ID [--output json] [-h, --help]
```
{: pre}

Where:

- **GATEWAY_ID**: ID of the gateway that the new connection will be on.
- **--name**: Name for the new connection.
- **--network-type**: Network type of the connection. Values are `vpc`, `directlink`, or `classic`.
- **--network-id**: ID of the network connection. For classic, do not set a value. For `vpc` and `directlink`, use the CRN. To find the CRN of a VPC:

   ```sh
   ibmcloud is vpc VPC_ID --json
   ```
   {: pre}

- **--network-account-id**: ID of the IBM Cloud account to use for creating a classic connection. Only used with 'classic' type, when the account of connection is different than the gateway's account.

- **--output json**: Optional: Specify if you want the output to display in JSON format.

- **--help | -h**: Optional: Get help on this command.

#### Examples
{: #connection-create-examples}

This example illustrates creating a VPC connection named `vpc-connection` using `vpcCRN="crn:v1:bluemix:public:is:us-south:a/3aa0a9999a1a46258064d84f7f447920::vpc:r134-f87014d5-87d2-46d1-9999-24683082f6bc"`:

```sh
ibmcloud tg cc $gateway --name vpc-connection --network-id $vpcCRN --network-type vpc
```
{: pre}

Create Classic connection named `classic-conn`.

```sh
ibmcloud tg cc $gateway --name classic-conn --network-type classic
```
{: pre}

## Adding a connection with the API
{: #tg-api-adding-connection-transit-gateway}
{: api}

To add a connection with the API, follow these steps:

1. Set up your [API environment](/docs/vpc?topic=vpc-set-up-environment#api-prerequisites-setup).
1. Store any additional variables to be used in the API commands.

### Request
{: ##tg-api-adding-connection-transit-gateway-request}

To add a connection to the transit gateway, adjust the following parameters:

| Path parameters | Details |
|--|--|
|**transit_gateway_id**  \n Required  \n string | The transit gateway identifier|
{: caption="Table 1. Path parameters for adding a connection" caption-side="bottom"}

|Query Parameters| Details |
|--|--|
|**version**  \n Required  \n string | Requests the version of the API as of a date in the format `YYYY-MM-DD`. Any date up to the current date may be provided. Specify the current date to request the latest version.  \n **Possible values:** Value must match regular expression  `^[0-9]{4}-[0-9]{2}-[0-9]{2}$`|
|**Request Body**  \n Required  \n TransitGatewayConnectionTemplate | The connection template|
|**network_type**  \n Required  \n string | Defines the type of network being connected to. For access to `gre_tunnel` connections, contact IBM support.  \n **Allowable values:** [`classic`,`directlink`,`gre_tunnel`,`unbound_gre_tunnel`,`vpc`]  \n **Example:** `vpc`|
|**base_connection_id**  \n string | The ID of an active transit gateway. `network_type` `gre_tunnel` connections must be created over an existing `network_type` `classic` connection. This field is required for `gre_tunnel` connections and must specify the ID of an active transit gateway network_type `classic` connection in the same transit gateway. Omit `base_connection_id` for any connection type other than `gre_tunnel`. \n **Example:** `975f58c1-afe7-469a-9727-7f3d720f2d32`|
|**base_network_type**  \n string | Defines the type of network the GRE tunnel is targeting. This field is required for, and only applicable to, `unbound_gre_tunnel` type connections.  \n **Allowable value:** [`classic`]  \n **Example:** `classic`|
|**local_gateway_ip**  \n string | The local gateway IP address. This field is required for, and only applicable to, `gre_tunnel` and `unbound_gre_tunnel` type connections.  \n **Example:** `192.168.100.1`|
|**local_tunnel_ip**  \n string | The local tunnel IP address. This field is required for, and only applicable to, `gre_tunnel` and `unbound_gre_tunnel` type connections. The `local_tunnel_ip` and `remote_tunnel_ip` addresses must be in the same `/30` network. Neither can be the network nor the broadcast addresses.  \n **Example:** `192.168.129.2`|
|**name**  \n Name|The user-defined name for this transit gateway connection. Network type `vpc` connections are defaulted to the name of the VPC. Network type `classic` connections are named 'Classic'.  \n Name specification is required for network `gre_tunnel` and `unbound_gre_tunnel` type connections.  \n **Possible values:** 1 ≤ length ≤ 63, Value must match regular expression `^([a-zA-Z]|[a-zA-Z][-_a-zA-Z0-9]*[a-zA-Z0-9])$`  \n **Example:** `Transit_Service_BWTN_SJ_DL`|
|**network_account_id**  \n AccountID | The ID of the account which owns the network that is being connected. Generally only used if the network is in a different account than the gateway. This field is required to be unspecified for network type `gre_tunnel`.  \n **Example:** `28e4d90ac7504be694471ee66e70d0d5`|
|**network_id**  \n string | The ID of the network being connected to via this connection. This field is required for some types, such as `vpc` and `directlink`. For network types `vpc` and `directlink` this is the CRN of the VPC / Direct Link gateway respectively. This field is required to be unspecified for `classic`, `gre_tunnel` and `unbound_gre_tunnel` type connections. \n **Example:** `crn:v1:bluemix:public:is:us-south:a/123456::vpc:4727d842-f94f-4a2d-824a-9bc9b02c523b`|
|**remote_bgp_asn**  \n string | The remote network BGP ASN. This field is only applicable to `gre_tunnel` and `unbound_gre_tunnel` type connections. The following ASN values are reserved and unavailable: `0`, `13884`, `36351`, `64512`, `64513`, `65100`, `65200–‍65234`, `65402‍–‍65433`, `65500`, and `4201065000‍–‍4201065999`. If `remote_bgp_asn` is omitted on `gre_tunnel` connection create requests, IBM will assign an ASN.  \n **Example:** `65010`|
|**remote_gateway_ip**  \n string | The remote gateway IP address. This field is required for, and only applicable to, `gre_tunnel` and `unbound_gre_tunnel` type connections.  \n **Example:** `10.242.63.12`|
|**remote_tunnel_ip**  \n string | The remote tunnel IP address. This field is required for, and only applicable to, `gre_tunnel` and `unbound_gre_tunnel` type connections. The `local_tunnel_ip` and `remote_tunnel_ip` addresses must be in the same `/30` network. Neither can be the network nor the broadcast addresses. \n **Example:** `192.168.129.1` |
|**zone**  \n ZoneIdentityByName | For `gre_tunnel` and `unbound_gre_tunnel` type connections, specify the connection's location. The specified availability zone must reside in the gateway's region. Use the IBM Cloud global catalog to list zones within the desired region. This field is required for, and only applicable to, network type `gre_tunnel` and `unbound_gre_tunnel` connections. |
|- **name**  \n string|Availability zone name.  \n **Example:** `us-south-1`|
{: caption="Table 2. Query parameters for adding a connection" caption-side="bottom"}

#### Example Request
{: ##tg-api-adding-connection-transit-gateway-request-example}

This example illustrates adding a connection to the transit gateway with the API:

```sh
curl -X POST --location --header "Authorization: Bearer {iam_token}" \
  --header "Accept: application/json" \
  --header "Content-Type: application/json" \
  --data '{ "network_type": "vpc" }'
  "
{base_url}/transit_gateways/{transit_gateway_id}/connections?version={version}"
```
{: pre}

```sh
  "base_connection_id": "975f58c1-afe7-469a-9727-7f3d720f2d32",
  "local_gateway_ip": "192.168.100.1",
  "local_tunnel_ip": "192.168.129.2",
  "name": "Transit_Service_BWTN_SJ_DL",
  "network_account_id": "28e4d90ac7504be694471ee66e70d0d5",
  "network_id": "crn:v1:bluemix:public:is:us-south:a/123456::vpc:4727d842-f94f-4a2d-824a-9bc9b02c523b",
  "network_type": "vpc",
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
```
{: screen}

### Response
{: #add-connection-curl-api-response}

The following response shows once you initiate the request:

| Response Body| Details |
|--|--|
|**name**  \n Always included*  \n Name|The user-defined name for this transit gateway connection.  \n **Possible values:** 1 ≤ length ≤ 63, Value must match regular expression  `^([a-zA-Z]|[a-zA-Z][-_a-zA-Z0-9]*[a-zA-Z0-9])$`  \n **Example:** `Transit_Service_BWTN_SJ_DL`|
|**network_type**  \n Always included*  \n string|Defines what type of network is connected via this connection. The list of enumerated values for this property may expand in the future. Code and processes using this field must tolerate unexpected values.  \n **Possible values:** [`classic`,`directlink`,`gre_tunnel`,`unbound_gre_tunnel`,`vpc`]  \n **Example:** `vpc`|
|**id**  \n Always included*  \n string | The unique identifier for this Transit Gateway Connection  \n **Example:** `1a15dca5-7e33-45e1-b7c5-bc690e569531`|
|**created_at** \n Always included*  \n date-time|The date and time that this connection was created|
|**network_id**  \n string|The ID of the network being connected via this connection. This field is required for some types, such as `vpc` and `directlink` For network types `vpc` and `directlink` it should be the CRN of the target vpc / gateway respectively.  \n **Example:** `crn:v1:bluemix:public:is:us-south:a/123456::vpc:4727d842-f94f-4a2d-824a-9bc9b02c523b`|
|**base_connection_id**  \n string|network_type `gre_tunnel` connections use `base_connection_id` to specify the ID of a network_type `classic` connection the tunnel is configured over. The specified connection must reside in the same transit gateway and be in an active state. The `classic` connection cannot be deleted until any `gre_tunnel` connections using it are deleted. This field only applies to and is required for network type `gre_tunnel` connections.  \n **Example:** `975f58c1-afe7-469a-9727-7f3d720f2d32`|
|**base_network_type**  \n string | Defines what type of network the GRE tunnel is targeting. This field is required for, and only applicable to, `unbound_gre_tunnel` type  connections.  \n **Allowable value:** [`classic`]  \n **Example:** `classic`|
|**local_bgp_asn** \n integer | The local network BGP ASN. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections. \n **Example:** `64490` |
|**local_gateway_ip** \n string | The local gateway IP address. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections. \n **Example:** `192.168.100.1` |
|**local_tunnel_ip** \n string | The local tunnel IP address. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections. \n **Example:** `192.168.129.2` |
|**mtu** \n integer | GRE tunnel MTU. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections. \n **Example:** `9000`|
|**network_account_id** \n AccountID|The ID of the account which owns the connected network. Generally only used if the network is in a different IBM Cloud account than the gateway.  \n **Example:** `28e4d90ac7504be694471ee66e70d0d5`|
|**remote_bgp_asn** \n integer | The remote network BGP ASN. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections. \n **Example:** `65010` |
|**remote_gateway_ip** \n string | The remote gateway IP address. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections. \n **Example:** `10.242.63.12`|
|**remote_tunnel_ip** \n string | The remote tunnel IP address. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections. \n **Example:** `192.168.129.1`|
|**request_status** \n string | Represents the status of a connection request between IBM Cloud accounts, and is only visible for cross account connections. The list of enumerated values for this property may expand in the future. Code and processes using this field must tolerate unexpected values. \n **Possible values:** [`pending`,`approved`,`rejected`,`expired`,`detached`]|
|**status**  \n string|Connection's current configuration state. The list of enumerated values for this property may expand in the future. Code and processes using this field must tolerate unexpected values.  \n **Possible values:** [`attached`,`failed`,`pending`,`deleting`,`detaching`,`detached`]|
|**updated_at**  \n date-time|The date and time that this connection was last updated|
|**zone**  \n ZoneReference | The location of the GRE tunnel. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|- **name**  \n Always included*  \n string|Availability zone name  \n **Example:** `us-south-1`|
{: caption="Table 3. Initiation request" caption-side="bottom"}

|Status Code||
|--|--|
|**201**|The Transit Gateway connection was created successfully.|
|**400**|An invalid connection template was provided.|
|**404**|The specified Transit Gateway could not be found, the specified resource group could not be found, or the default resource group could not be found (if the resource group was not specified in the template).|
|**409**|The network being connected must either be in a location that is considered "local" to the specified Transit Gateway, or the specified Transit Gateway needs to be global. The network being connected cannot already be connected to another Transit Gateway.|
{: caption="Table 4. Status codes" caption-side="bottom"}

#### Example Response
{: #add-connection-curl-api-response-example}

This example response illustrates that the connection was created successfully:

```sh
{
  "name": "Transit_Service_BWTN_SJ_DL",
  "network_id": "crn:v1:bluemix:public:is:us-south:a/123456::vpc:4727d842-f94f-4a2d-824a-9bc9b02c523b",
  "network_type": "vpc",
  "id": "1a15dca5-7e33-45e1-b7c5-bc690e569531",
  "base_connection_id": "975f58c1-afe7-469a-9727-7f3d720f2d32",
  "created_at": "2022-02-18T16:51:50.748Z",
  "local_bgp_asn": 64490,
  "local_gateway_ip": "192.168.100.1",
  "local_tunnel_ip": "192.168.129.2",
  "mtu": 9000,
  "network_account_id": "28e4d90ac7504be694471ee66e70d0d5",
  "prefix_filters": [
    {
      "action": "permit",
      "before": "1a15dcab-7e40-45e1-b7c5-bc690eaa9782",
      "created_at": "2022-02-18T16:51:50.748Z",
      "ge": 0,
      "id": "1a15dcab-7e30-45e1-b7c5-bc690eaa9865",
      "le": 32,
      "prefix": "192.168.100.0/24",
      "updated_at": "2022-02-18T16:51:50.748Z"
    }
  ],
  "prefix_filters_default": "permit",
  "remote_bgp_asn": 65010,
  "remote_gateway_ip": "10.242.63.12",
  "remote_tunnel_ip": "192.168.129.1",
  "request_status": "pending",
  "status": "attached",
  "updated_at": "2022-02-18T16:51:50.748Z",
  "zone": {
    "name": "us-south-1"
  }
}
```
{: screen}

For more information (including Java, Node, Python and Go examples), see "Add Connection to a Transit Gateway" in the [Transit Gateway API reference](/apidocs/transit-gateway?code=java#create-transit-gateway-connection).
{: note}

## Adding a connection using Terraform
{: #tg-terraform-adding-connection-transit-gateway}
{: terraform}

Review the following argument references that you can specify for your resource when creating a connection for a transit gateway using Terraform:

|Argument|Details|
|--|--|
|**base_connection_id**  \n Optional  \n Forces new resource \n string | The ID of a network_type 'classic' connection a tunnel is configured over.  \n This field only applies to network type `gre_tunnel` connections.|
|**base_network_type**  \n Optional  \n Forces new resource  \n string | The base network type. Allowed values are `classic`.  \n This field only applies to `unbound_gre_tunnel` type connections.
|**gateway**  \n Required  \n Forces new resource  \n string | Enter the transit gateway identifier.|
|**local_gateway_ip**  \n Optional  \n Forces new resource  \n string | The local gateway IP address. \n This field is required for, and only applicable to, `gre_tunnel` and `unbound_gre_tunnel` type connections. |
|**local_tunnel_ip**  \n Optional  \n Forces new resource  \n string | The local tunnel IP address. \n This field is required for, and only applicable to, `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**name**  \n Optional  \n string | The connection name. If the name is not given, a default name is provided based on the network type, such as `vpc` for network type VPC and `classic` for network type classic.|
|**network_account_id**  \n Optional  \n Forces new resource  \n string|The ID of the network connected account. This is used if the network is in a different account than the gateway.|
|**network_type**  \n Required  \n Forces new resource  \n string | The network type. Allowed values are `classic`, `directlink`, `gre_tunnel`, `unbound_gre_tunnel`, and `vpc`. |
|**network_id**  \n Optional  \n Forces new resource  \n string | The ID of the network being connected to through this connection. \n This parameter is required for network type `vpc` and `directlink`, the CRN of the VPC or direct link gateway to be connected.  \n This field is required to be unspecified for network type `classic`.  \n **Example**:`crn:v1:bluemix:public:is:us-south:a/123456::vpc:4727d842-f94f-4a2d-824a-9bc9b02c523b`|
|**remote_bgp_asn**  \n Optional  \n Forces new resource  \n integer | The remote network BGP ASN (will be generated for the connection if not specified).  \n This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**remote_gateway_ip**  \n Optional  \n Forces new resource  \n string | The remote gateway IP address. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**remote_tunnel_ip**  \n Optional  \n Forces new resource  \n string | The remote tunnel IP address. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**zone**  \n Optional  \n Forces new resource  \n string | The location of the GRE tunnel. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections. |
{: caption="Table 5. Terraform argument references for creating a connection" caption-side="bottom"}

### Example
{: #tg-terraform-adding-connection-transit-gateway-example}

This example illusstrates creating a transit gateway connection using Terraform:

```sh
resource "ibm_tg_connection" "test_ibm_tg_connection" {
  gateway      = ibm_tg_gateway.test_tg_gateway.id
  network_type = "vpc"
  name         = "myconnection"
  network_id   = ibm_is_vpc.test_tg_vpc.resource_crn
}
```
{: pre}
