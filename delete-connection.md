---

copyright:
  years: 2020, 2025
lastupdated: "2025-10-01"

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
1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**.
1. Click the name of the transit gateway where you want to delete a connection.

   If you are in the expanded view, click **View details**.
   {: tip}

1. From the Connections page, click the Actions menu ![Actions menu](../../icons/action-menu-icon.svg) next to the connection that you want to delete and select **Delete**.

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

You can delete a connection with the API.

After the specified connection is detached, entities still within the transit gateway will no longer be able to communicate directly to it through the IBM Cloud private backbone.
{: note}

### Example Request
{: #deleting-connections-api-request-example}

This example request illustrates deleting a connection:

```sh
curl -X DELETE "https://transit.cloud.ibm.com/v1/transit_gateways/$TRANSIT_GATEWAY_ID/connections/$CONNECTION_ID?version=2022-02-09" -H "accept: */*"
```
{: pre}

### Example Response
{: #example-returned-response}

This example illustrates the returned response when the connection could not be found:

```json
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

For more information, see [Removes a connection from Transit Gateway](/apidocs/transit-gateway#delete-transit-gateway-connection) in the Transit Gateway API reference.
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
