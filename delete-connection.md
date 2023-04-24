---

copyright:
  years: 2020, 2022
lastupdated: "2022-02-16"

keywords: editing, managing, manage, edit, add, connection

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Deleting a connection
{: #deleting-connections}

## Deleting a connection in the UI
{: #deleting-connections-ui}
{: ui}

To delete a connection from a transit gateway, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Interconnectivity**.
1. Click **Transit Gateway** from the left navigation pane.
1. Click the name of the transit gateway where you want to delete a connection.

   If you are in the expanded view, click **View details**.
   {: tip}

1. From the Connections page, click the Actions menu ![Actions menu](/images/overflow.png) next to the connection that you want to delete and select **Delete**.

## Deleting a connection from the CLI
{: #deleting-connections-cli}
{: cli}

You can delete an existing connection with the CLI with the following command:

```sh
ibmcloud tg connection-delete|cd GATEWAY_ID CONNECTION_ID [-f, --force] [-h, --help]
```
{: pre}

Where:

- **GATEWAY_ID**: ID of the gateway of the connection being deleted.

- **CONNECTION_ID**: ID of the connection being deleted.

- **--force | -f**: Optional: Force the delete without confirmation.

- **--help | -h**: Optional: Get help on this command.

### Example
{: #connection-delete-example}

This example illustrates deleting a connection without confirmation:

```sh
ibmcloud tg cd $gateway $connection -f
```
{: pre}

## Deleting a connection with the API
{: #deleting-connections-api}
{: api}

After the specified connection is detached, entities still within the transit gateway will no longer be able to communicate directly to it through the IBM Cloud private backbone.
{: note}

You can delete a connection with the API.

### Request 
{: #deleting-connections-api-request}

To delete a connection with the API, set the following parameters:

|Path Parameters|Details|
|--|--|
|**transit_gateway_id**  \n Required  \n string|The Transit Gateway identifier|
|**id**  \n Required  \n string|The connection identifier|
{: caption="Table 1. Path parameters for deleting a connection" caption-side="bottom"}

|Query Parameters|Details|
|--|--|
|**version**  \n Required  \n string|Requests the version of the API as of a date in the format `YYYY-MM-DD`. Any date up to the current date may be provided. Specify the current date to request the latest version.  \n **Possible values:** Value must match regular expression  `^[0-9]{4}-[0-9]{2}-[0-9]{2}$`|
{: caption="Table 1. Query parameters for deleting a connection" caption-side="bottom"}

#### Example Request
{: #deleting-connections-api-request-example}

This example request illustrates deleting a connection:

```sh
DELETE /transit_gateways/{transit_gateway_id}/connections/{id}

"{base_url}/transit_gateways/{transit_gateway_id}/connections/{id}?version={version}"

curl -X DELETE "https://transit.cloud.ibm.com/v1/transit_gateways/testgateway/connections/testconnection?version=2022-02-09" -H "accept: */*"
```
{: pre}

### Response
{: #deleting-connections-api-response}

The following status codes will be returned:

|Status code||
|--|--|
|**200**|The connection was removed successfully.|
|**404**|A Transit Gateway or Transit Gateway connection with the specified identifier could not be found.|
{: caption="Table 1. Status codes for deleting a connection" caption-side="bottom"}

#### Example Response
{: #example-returned-response}

This example illustrates the returned response when the connection could not be found:

```sh
{
  "errors": [
    {
      "code": "not_found",
      "message": "Cannot find Connection",
      "more_info": "https://cloud.ibm.com/apidocs/transit-gateway#error-handling"
    }
  ],
  "trace": "request_id"
}
```
{: pre}

For more information (including Java, Node, Python and Go examples), see "Remove connection from Transit Gateway" in the [Transit Gateway API reference](/apidocs/transit-gateway#delete-transit-gateway-connection).
{: note}

## Deleting a connection using Terraform
{: #deleting-connections-terraform}
{: terraform}

To delete a connection, perform the following command:

```sh
terraform destroy -target=resource_type.resource_name
```
{: pre}

Where:

- **resource_type**: ibm_tg_connection

- **resource_name**: Name of connection

### Example
{: #deleting-connections-terraform-example}

This example illustrates deleting a connection using Terraform:

```sh
terraform destroy -target=ibm_tg_connection.test_ibm_tg_connection
```
{: pre}
