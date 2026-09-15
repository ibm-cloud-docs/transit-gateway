---

copyright:
  years: 2020, 2026
lastupdated: "2026-09-15"

keywords: editing, managing, manage, edit, add, connection

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Changing your configuration
{: #change-configuration}

You can change your transit gateway name, routing type, and other settings by using the UI, CLI, API, or Terraform.
{: shortdesc}

## Changing your configuration in the UI
{: #change-configuration-ui}
{: ui}

To change your transit gateway configuration in the UI, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**.
1. Click the name of the transit gateway that you want to edit.

   If you are in the expanded view, click **View details**.

1. From the Connections page, click **Actions**, then select **Edit**.

   From here, you can:

   * Change the gateway's name and its routing type (local or global).
   * Enable or disable route propagation across all GREs connected to the same transit gateway.

      Changes to route propagation or routing type can take several minutes to apply, depending on the number of existing connections.

   * Update the redundancy group name.

      * The redundancy group field is available only when global routing is enabled.
      * The redundancy group is a shared configuration. Renaming the group updates it across all associated transit gateways.
      * You must have permissions to edit each transit gateway in the redundancy group to update the group name.

   Routing type considerations:

   * To switch to a different routing type, you must delete any connections that aren't local to the transit gateway’s location.
   * When you change from local to global routing for a specific transit gateway, you are charged for all associated connection traffic.
   * The transit gateway must have fewer than 30 connections to change the routing type.

## Changing your configuration from the CLI
{: #change-configuration-cli}
{: cli}

To update properties on an existing gateway from the CLI, run the following command:

```sh
ibmcloud tg gateway-update|gwu GATEWAY_ID [--name NAME] [--routing ROUTING] [--redundancy-group GROUP_NAME] [--gre-enhanced-route-propagation true | false] [--output json] [-h, --help]
```
{: pre}

Where:

`GATEWAY_ID`
:   ID of the gateway you want to update.

`--name`
:   Optional: New name of the gateway.

`--routing`
:   Optional: Gateway routing of resources (`global` | `local`). Select `global` to connect resources across regions. Changing routing from `global` to `local` requires all existing connections to be local.

 This cannot be changed if the gateway is in a redundancy group.

`--redundancy-group`
:   Optional: Updates the name of the redundancy group that the gateway belongs to. Only valid when the gateway is already in a redundancy group and global routing is enabled. Renaming the group updates it for all associated transit gateways.

`--gre-enhanced-route-propagation`
:   Optional: Specify whether you want to enable or disable route propagation across all GREs connected to the same transit gateway. One of: `true` or `false` (default)

`--output json`
:   Optional: Specify whether you want the output displayed in JSON format.

`--help | -h`
:   Optional: Get help on this command.

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

{
  "global": true,
  "name": "my-transit-gateway",
  "redundancy_group": {
    "name": "my-redundancy-group"
  }
}
```
{: pre}

### Example Response
{: #change-configuration-api-response-example}

This response indicates that the transit gateway was updated successfully:

```json
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

For more information, see [Updates specified Transit Gateway](/docs/apis/transit-gateway#update-transit-gateway) in the Transit Gateway API reference.
{: note}

## Changing your configuration by using Terraform
{: #change-configuration-terraform}
{: terraform}

You can specify the following argument references for your resource when you change the configuration of your transit gateway by using Terraform:

|Argument|Details|
|--|--|
|**name**  \n Required  \n string | The unique user-defined name for the gateway. For example, `myGateway`|
|**global**  \n Required  \n boolean|The gateways with global routing (true) are able to connect to the networks outside their associated region.|
| **redundancy_group**  \n Optional  \n string | Specifies the redundancy group for a global transit gateway. Only valid if the transit gateway already is in a redundancy group. If the redundancy group name is different, the redundancy group name will change.|
|**gre_enhanced_route_propagation** \n Optional  \n boolean| Specify whether you want to enable or disable route propagation across all GREs connected to the same transit gateway. Values are one of: `true` or `false` (default) |
{: caption="Terraform argument references for changing the configuration" caption-side="bottom"}

### Example
{: #change-configuration-terraform-example}

This example illustrates changing the configuration of your transit gateway:

```terraform
resource "ibm_tg_gateway" "new_tg_gw"{
 name="transit-gateway-1"
 location="us-south"
 global=true
 redundancy_group="group1"
 gre_enhanced_route_propagation=false
 resource_group="30951d2dff914dafb26455a88c0c0092"
}
```
{: codeblock}

The `redundancy_group` attribute requires the transit gateway to be already in a redundancy group. If the redundancy group name is different, the redundancy group will be renamed if no redundancy group with that name in the account exists.
{: important}
