---

copyright:
  years: 2020, 2022
lastupdated: "2022-02-17"

keywords: deleting, delete

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Deleting a transit gateway
{: #delete-gateway}
{: help}
{: support}

## Deleting a transit gateway in the UI
{: #delete-gateway-ui}
{: ui}

To delete an {{site.data.keyword.tg_full}}, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) on the upper left of the page, then click **Interconnectivity**.
1. Click **Transit Gateway**.
1. Click the name of the transit gateway you want to delete.
1. Ensure the transit gateway has no attached connections - if it does, delete all connections.
   For each connection you want to delete, click the Actions menu next to it, then select **Delete**.
1. After the connections are removed, you can delete the transit gateway in two ways:

   * From the transit gateway's details page, click the Actions menu ![Actions menu](/images/overflow.png) next to the gateway you want to delete and select **Delete**.
   * From an individual transit gateway page, select **Actions > Delete**.

## Deleting a transit gateway from the CLI
{: #delete-gateway-cli}
{: cli}

To delete an existing gateway from the CLI, enter the following command:

```sh
ibmcloud tg gateway-delete|gwd GATEWAY_ID [-f, --force] [-h, --help]
```
{: pre}

Where:

- **GATEWAY_ID**: ID of the gateway you want to delete.

- **--force | -f**: Optional: Force the delete without confirmation.

- **--help | -h**: Optional: Get help on this command.

### Example
{: #tgw-delete-examples}

This example illustrates deleting a gateway with no confirmation:

```sh
ibmcloud tg gwd $gateway -f
```
{: pre}

## Deleting a transit gateway with the API
{: #delete-gateway-api}
{: api}

To delete a transit gateway with the API, follow these steps:

1. Remove all connections from the transit gateway.
1. Request the deletion of the gateway with the API.

### Request
{: #delete-gateway-api-request}

To delete a transit gateway, set the following parameters:

|Path parameters|Details|
|--|--|
|**id**  \n Required  \n string|The Transit Gateway identifier|
{: caption="Table 1. Path parameters for deleting a transit gateway" caption-side="bottom"}

|Query parameters|Details|
|--|--|
|**version**  \n Required  \n string|Requests the version of the API as of a date in the format `YYYY-MM-DD`. Any date up to the current date can be provided. Specify the current date to request the latest version.  \n **Possible values:** Value must match regular expression  `^[0-9]{4}-[0-9]{2}-[0-9]{2}$`|
{: caption="Table 2. Query parameters for deleting a transit gateway" caption-side="bottom"}

#### Example request
{: #delete-gateway-api-request-example}

This example iiilustrates a transit gateway deletion request:

```sh
DELETE /transit_gateways/{id}

"{base_url}/transit_gateways/{id}?version={version}"

curl -X DELETE "https://transit.cloud.ibm.com/v1/transit_gateways/testgateway?version=2022-02-10" -H "accept: */*"
```
{: pre}

### Response
{: #delete-gateway-api-response}

The following status codes will be returned:

|Status code|Details|
|--|--|
|**204**|The transit gateway was deleted successfully.|
|**404**|A transit gateway with the specified identifier could not be found.|
|**409**|The transit gateway could not be deleted as there are pre-existing connections attached.|
{: caption="Table 3. Status codes when deleting a transit gateway" caption-side="bottom"}

#### Example response
{: #delete-gateway-api-response-example}

This example illustrates that the transit gateway could not be found, leading to a Status 404 response:

```sh
{
  "errors": [
    {
      "code": "not_found",
      "message": "Cannot find Gateway",
      "more_info": "https://cloud.ibm.com/apidocs/transit-gateway#error-handling"
    }
  ],
  "trace": "request_id"
}
```
{: pre}

For more information (including Java, Node, Python and Go examples), see "Deletes Specified Transit Gateway" in the [Transit Gateway API reference](/apidocs/transit-gateway#delete-transit-gateway).
{: note}

## Deleting a transit gateway using Terraform
{: #delete-gateway-terraform}
{: terraform}

To delete a transit gateway, enter the following command:

```sh
terraform destroy -target=resource_type.resource_name
```
{: pre}

Where:

- **resource_type**: ibm_tg_gateway

- **resource_name**: Name of transit gateway

### Example
{: #delete-gateway-terraform-example}

This example illustrates deleting a transit gateway named "new_tg_gw":

```sh
terraform destroy -target=ibm_tg_gateway.new_tg_gw
```
{: pre}
