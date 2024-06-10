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
1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Interconnectivity** > **Transit Gateway**.
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

For more information (including Java, Node, Python and Go examples), see "Deletes specified Transit Gateway" in the [Transit Gateway API reference](/apidocs/transit-gateway#delete-transit-gateway).
{: note}
 
### Example request
{: #delete-gateway-api-request-example}

This example iiilustrates a transit gateway deletion request:

```sh
curl -X DELETE "https://transit.cloud.ibm.com/v1/transit_gateways/$TRANSIT_GATEWAY_ID?version=2022-02-10" -H "accept: */*"
```
{: pre}

### Example response
{: #delete-gateway-api-response-example}

This example illustrates that the transit gateway could not be found, leading to a Status 404 response:

```json
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
