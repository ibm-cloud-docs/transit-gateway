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
1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Interconnectivity** > **Transit Gateway**.
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

### Example Request
{: #editing-connections-api-request-example}

This example illustrates editing the name of a transit gateway connection:

```sh
curl -H "Content-Type: application/json" -X PATCH https://$TS_ENDPOINT/v1/transit_gateways/$GATEWAY_ID/connections/$CONNECTION_ID?version=2020-03-31   -H "authorization: Bearer $IAM_TOKEN"   -d '{
  "name":  "Transit_Service_BWTN_SJ_DL",
  "prefix_filters_default":  "permit"
}'
```
{: pre}

### Example Response
{: #editing-connections-api-response-example}

The following response indicates that the connection was updated successfully:

```json
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


For more information, see [Updates specified Transit Gateway connection](/apidocs/transit-gateway#update-transit-gateway-connection) in the Transit Gateway API reference.
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
{: #edit-configuration-terraform-example}

This example illustrates editing a transit gateway connection in Terraform:

```sh
resource "ibm_tg_connection" "test_ibm_tg_connection" {
  gateway      = ibm_tg_gateway.test_tg_gateway.id
  network_type = "vpc"
  name         = "myconnection"
}
```
{: pre}
