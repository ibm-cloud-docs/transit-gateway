---

copyright:
  years: 2020, 2025
lastupdated: "2025-05-29"

keywords: editing, managing, manage, edit, add, connection

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Changing your configuration
{: #change-configuration}

## Changing your configuration in the UI
{: #change-configuration-ui}
{: ui}

To change your transit gateway configuration in the UI, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**.
1. Click the name of the transit gateway that you want to edit.

   If you are in the expanded view, click **View details**.

1. From the Connections page, click **Actions** in the upper right, then select **Edit**.

   From here, you can change the gateway's name and its routing type (Local or Global). 

   To change a transit gateway's routing type from Global to Local, you must delete any connections that aren't local to the transit gateway's location.
   {: tip}

   When you change from Local to Global routing for a specific transit gateway, you are charged for all associated connection traffic.
   {: important}

## Changing your configuration from the CLI
{: #change-configuration-cli}
{: cli}

To update properties on an existing gateway from the CLI, run the following command:

```sh
ibmcloud tg gateway-update|gwu GATEWAY_ID [--name NAME] [--routing ROUTING] [--output json] [-h, --help]
```
{: pre}

Where:

- **GATEWAY_ID**: ID of the gateway you want to update.

- **--name**: Optional: New name of the gateway.

- **--routing**: Optional: Gateway routing of resources (`global` | `local`). Select `global` to connect resources across regions. Changing routing from `global` to `local` requires all existing connections to be local.

- **--output JSON**: Optional: Specify whether you want the output that is displayed in JSON format.

- **--help | -h**: Optional: Get help on this command.

### Example
{: #gateway-update-example}

This example illustrates updating a gateway with a routing value of `global`:

```sh
ibmcloud tg gwu $gateway --routing global
```
{: pre}

## Changing your configuration with the API
{: #change-configuration-api}
{: api}

You can update your transit gateway's name, global parameters, or both with the API.

### Example Request
{: #change-configuration-api-request-example}

This example illustrates changing your configuration with the API:

```sh
PATCH /transit_gateways/{id}
"{base_url}/transit_gateways/{id}?version={version}"
{
  "global": true,
  "name": "my-transit-gateway"
}
```
{: pre}

### Example Response
{: #change-configuration-api-response-example}

This response indicates that the transit gateway was updated successfully:

```sh
{
  "created_at": "2020-03-31T12:08:05Z",
  "crn": "crn:[...]",
  "global": false,
  "id": "ef4dcb1a-fee4-41c7-9e11-9cd99e65c1f4",
  "location": "us-south",
  "name": "example-gateway-new-name",
  "resource_group": {
    "id": "56969d6043e9465c883cb9f7363e78e8"
  },
  "status": "available",
  "updated_at": "2020-03-31T12:08:05Z"
}
```
{: screen}

For more information, see [Updates specified Transit Gateway](/apidocs/transit-gateway#update-transit-gateway) in the Transit Gateway API reference.
{: note}

## Changing your configuration by using the Terraform
{: #change-configuration-terraform}
{: terraform}

You can specify the following argument references for your resource when you change the configuration of your transit gateway by using Terraform:

|Argument|Details|
|--|--|
|**name**  \n Required  \n Boolean | The unique user-defined name for the gateway. For example, `myGateway`|
|**global**  \n Required  \n Boolean|The gateways with global routing (true) to connect to the networks outside their associated region.|
{: caption="Terraform argument references for changing the configuration" caption-side="bottom"}

### Example
{: #change-configuration-terraform-example}

This example illustrates changing the configuration of your transit gateway:

```sh
resource "ibm_tg_gateway" "new_tg_gw"{
name="transit-gateway-1"
location="us-south"
global=true
resource_group="30951d2dff914dafb26455a88c0c0092"
}
```
{: pre}
