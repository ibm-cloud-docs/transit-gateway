---

copyright:
  years: 2026
lastupdated: "2026-09-15"

keywords:

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Using redundancy groups
{: #using-redundancy-groups}

You manage redundancy groups by creating or updating transit gateways that share a group name. A redundancy group is not a separate resource. Instead, it is a shared configuration that is defined on each transit gateway.
{: shortdesc}

Before configuring redundancy groups, review [Redundancy group considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips) to ensure that your network connections and routing are configured correctly for redundancy.
{: important}

## Viewing redundancy group information
{: #viewing-redundancy-groups}
{: ui}

You can view redundancy group information for a transit gateway in the following locations:

- **Transit Gateway list view** – Displays the redundancy group for each gateway.
- **Transit Gateway details page** – Shows the redundancy group that is assigned to the gateway.

The redundancy group is displayed only for transit gateways that use global routing.

## Viewing redundancy group information from the CLI
{: #viewing-redundancy-groups-cli}
{: cli}

### Viewing redundancy group assigned to transit gateway
{: #viewing-redundancy-groups-tgw-cli}

To view the redundancy group that is assigned to a transit gateway, use the `gateway` command and check the `redundancy_group` field in the output.

```sh
ibmcloud tg gateway GATEWAY_ID [--output json]
```
{: pre}

Where:

`GATEWAY_ID`
:   The ID of the transit gateway to retrieve.

`--output json`
:   Optional: Specify whether you want the output displayed in JSON format.

The redundancy group is displayed only for transit gateways that use global routing.

### Viewing list of redundancy groups in account
{: #viewing-redundancy-groups-list-cli}

To view the redundancy groups in an account, use the `redundancy-groups` command.

```sh
ibmcloud tg redundancy-groups [--output json]
```
{: pre}

Where:

`--output json`
:   Optional: Specify whether you want the output displayed in JSON format.

### Viewing a redundancy group
{: #viewing-redundancy-group-cli}

To view a redundancy group in an account, use the `redundancy-group` command.

```sh
ibmcloud tg redundancy-groups REDUNDANCY_GROUP_ID [--output json]
```
{: pre}

Where:

`REDUNDANCY_GROUP_ID`
:   The ID of the redundancy group to retrieve.

`--output json`
:   Optional: Specify whether you want the output displayed in JSON format.

### Renaming a redundancy group
{: #rename-redundancy-group-cli}

To rename a redundancy group in an account, use the `redundancy-group-update` command.

```sh
ibmcloud tg redundancy-group-update REDUNDANCY_GROUP_ID --name NEW_NAME [--output json]
```
{: pre}

Where:

`REDUNDANCY_GROUP_ID`
:   The ID of the redundancy group to retrieve.

`--name NEW_NAME`
:   The new name of the redundancy group.

`--output json`
:   Optional: Specify whether you want the output displayed in JSON format.

The new name cannot be already used by an existing redundancy group in the account.


## Viewing redundancy group information with the API
{: #viewing-redundancy-groups-api}
{: api}

To view the redundancy group that is assigned to a transit gateway, call the `GET /transit_gateways/{id}` method and check the `redundancy_group` field in the response.

```sh
GET /transit_gateways/{id}
```
{: pre}

The response includes a `redundancy_group` field when the transit gateway belongs to a redundancy group. The field is only present for transit gateways that use global routing.

## Viewing redundancy group information with Terraform
{: #viewing-redundancy-groups-terraform}
{: terraform}

To view the redundancy group that is assigned to a transit gateway, use the `ibm_tg_gateway` data source and reference the `redundancy_group` attribute.

```terraform
data "ibm_tg_gateway" "example" {
  name = "transit-gateway-1"
}

output "redundancy_group" {
  value = data.ibm_tg_gateway.example.redundancy_group
}
```
{: codeblock}

The `redundancy_group` attribute is only populated for transit gateways that use global routing.

## Creating a redundant global transit gateway in the console
{: #create-redundant-global-tgw-ui}
{: ui}

You can create a redundant global transit gateway by creating a new gateway and assigning it to a new or existing redundancy group.

To create a redundant global transit gateway in the IBM Cloud console, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**.
1. Click **Create gateway**.
1. Select **Global routing** (required for redundancy groups).
1. Enter a **Redundancy group** name. Enter a new name to create a new group, or select an existing group to add this new gateway to it.
1. Complete the remaining gateway configuration and click **Create**.

## Converting an existing global transit gateway to a redundant global transit gateway in the console
{: #convert-global-tgw-ui}
{: ui}

You can convert an existing global transit gateway into a redundant global transit gateway by assigning it to a new redundancy group.

An existing global transit gateway cannot be added to an existing redundancy group. To convert an existing global transit gateway, you must create a new redundancy group.
{: important}

To convert an existing global transit gateway in the IBM Cloud console, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**.
1. Select the existing global transit gateway that you want to convert.
1. Click **Edit**.
1. Enter a new **Redundancy group** name to create a new redundancy group for this gateway.
1. Click **Save**.

## Creating a redundant global transit gateway from the CLI
{: #create-redundant-global-tgw-cli}
{: cli}

You can create a redundant global transit gateway by specifying a redundancy group name or ID at creation time. If you specify a name that does not exist, a new group is created. If the group already exists, the new gateway joins that group.

```sh
ibmcloud tg gateway-create --name NAME --location LOCATION \
  --routing global \
  --redundancy-group GROUP_NAME
```
{: pre}

Or, if the redundancy group already exists and you want to specify it by ID:

```sh
ibmcloud tg gateway-create --name NAME --location LOCATION \
  --routing global \
  --redundancy-group-id GROUP_ID
```
{: pre}

Where:

`--redundancy-group`
:   Specifies the redundancy group for this new gateway by name. If the group name does not exist, a new group is created. If the group already exists, this new gateway joins it.

    Valid only when `--routing global` is specified.

`--redundancy-group-id`
:   Specifies the ID of an existing redundancy group to join. Use this option instead of `--redundancy-group` when the group already exists and you prefer to reference it by ID.

    Valid only when `--routing global` is specified.

## Converting an existing global transit gateway to a redundant global transit gateway from the CLI
{: #convert-global-tgw-cli}
{: cli}

You can convert an existing global transit gateway into a redundant global transit gateway by updating the gateway with a new redundancy group name.

An existing global transit gateway cannot be added to an existing redundancy group. To convert an existing global transit gateway, you must create a new redundancy group.
{: important}

```sh
ibmcloud tg gateway-update GATEWAY_ID \
  --redundancy-group NEW_GROUP_NAME
```
{: pre}

Where:

`GATEWAY_ID`
:   The ID of the existing global transit gateway to convert.

`--redundancy-group NEW_GROUP_NAME`
:   The name of the new redundancy group to create for this gateway. The name must not already exist in the account.

## Creating a redundant global transit gateway with the API
{: #create-redundant-global-tgw-api}
{: api}

Create a redundant global transit gateway by including the `redundancy_group` field in the create request. If the group name does not exist, a new group is created. If it exists, the new gateway joins that group.

```sh
POST /transit_gateways

{
  "name": "example-tg",
  "location": "us-south",
  "global": true,
  "redundancy_group": "group1"
}
```
{: pre}

## Converting an existing global transit gateway to a redundant global transit gateway with the API
{: #convert-global-tgw-api}
{: api}

You can convert an existing global transit gateway into a redundant global transit gateway by patching the gateway with a new redundancy group name.

An existing global transit gateway cannot be added to an existing redundancy group. To convert an existing global transit gateway, you must create a new redundancy group.
{: important}

```sh
PATCH /transit_gateways/{id}

{
  "redundancy_group": "new-group-name"
}
```
{: pre}

The `redundancy_group` value must be a name that does not already exist in the account.

## Creating a redundant global transit gateway with Terraform
{: #create-redundant-global-tgw-terraform}
{: terraform}

Create a redundant global transit gateway by specifying the `redundancy_group` attribute in your Terraform configuration. If the group does not exist, it is created. If it exists, the new gateway joins that group.

```terraform
resource "ibm_tg_gateway" "example" {
  name             = "transit-gateway-1"
  location         = "us-south"
  global           = true
  redundancy_group = ibm_tg_redundancy_group.new_tg_rg
}

resource "ibm_tg_redundancy_group" "new_tg_rg" {
  name = "group-1"
}
```
{: codeblock}

The `redundancy_group` attribute requires `global = true`.
{: important}

## Converting an existing global transit gateway to a redundant global transit gateway with Terraform
{: #convert-global-tgw-terraform}
{: terraform}

You can convert an existing global transit gateway into a redundant global transit gateway by adding the `redundancy_group` attribute to the existing gateway resource and creating a new `ibm_tg_redundancy_group` resource.

An existing global transit gateway cannot be added to an existing redundancy group. To convert an existing global transit gateway, you must create a new redundancy group.
{: important}

```terraform
resource "ibm_tg_gateway" "existing_example" {
  name             = "existing-transit-gateway"
  location         = "us-south"
  global           = true
  redundancy_group = ibm_tg_redundancy_group.new_tg_rg
}

resource "ibm_tg_redundancy_group" "new_tg_rg" {
  name = "new-group-name"
}
```
{: codeblock}

After updating your configuration, run:

```sh
terraform apply
```
{: pre}

## Renaming a redundancy group in the console
{: #rename-redundancy-group-ui}
{: ui}

To rename a redundancy group, update the redundancy group name on any transit gateway in the group.

The redundancy group name is a shared configuration. Renaming the group updates the name across all transit gateways in the group.
{: important}

To rename a redundancy group, you must have sufficient permissions to edit all transit gateways in the group.

To rename a redundancy group in the IBM Cloud console, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**.
1. Select a transit gateway that is part of the redundancy group.
1. Click **Edit**.
1. Update the **Redundancy group** name.
1. Click **Save**.

Renaming the redundancy group updates the name across all transit gateways in the group.
{: important}

## Renaming a redundancy group from the CLI
{: #rename-redundancy-group-from-cli}
{: cli}

To rename a redundancy group, use the `ibmcloud tg redundancy-group-update` command. You must have sufficient permissions to edit all transit gateways in the group.

The redundancy group name is a shared configuration. Renaming the group updates the name across all transit gateways in the group.
{: important}

```sh
ibmcloud tg redundancy-group-update NAME --name NEW_NAME [--output json] [-h, --help]
```
{: pre}

Where:

`NAME`
:   The name of the redundancy group you want to update.

`--name NEW_NAME`
:   The new name for the redundancy group. Cannot use a name that is already in use in the account.

`--output json`
:   Optional: Specify whether you want the output displayed in JSON format.

`--help | -h`
:   Optional: Get help on this command.

### Example
{: #rename-redundancy-group-cli-example}

```sh
ibmcloud tg rgu $redundancy_group --name NEW_NAME
```
{: pre}

## Renaming a redundancy group with the API
{: #rename-redundancy-group-api}
{: api}

To rename a redundancy group, update the `redundancy_group` field on any transit gateway in the group. You must have sufficient permissions to edit all transit gateways in the group.

The redundancy group name is a shared configuration. Renaming the group updates the name across all transit gateways in the group.
{: important}

```sh
PATCH /redundancy_groups/{id}

{
  "name": "new-group-name"
}
```
{: pre}

Updating the `name` value renames the redundancy group across all associated transit gateways.
{: important}

## Renaming a redundancy group with Terraform
{: #rename-redundancy-group-terraform}
{: terraform}

To rename a redundancy group, update the `name` attribute in the `ibm_tg_redundancy_group` resource in your Terraform configuration along with the TGW resource configuration and apply the changes. You must have sufficient permissions to edit all transit gateways in the group.

The redundancy group name is a shared configuration. Renaming the group updates the name across all transit gateways in the group.
{: important}

```terraform
resource "ibm_tg_gateway" "example" {
  name             = "transit-gateway-1"
  location         = "us-south"
  global           = true
  redundancy_group = ibm_tg_redundancy_group.tg_rg
}

resource "ibm_tg_redundancy_group" "tg_rg"{
name="new-name"
}
```
{: codeblock}

After updating your configuration, run:

```sh
terraform apply
```
{: pre}

Updating the `ibm_tg_redundancy_group` name attribute renames the group across all associated transit gateways.
{: important}

## Removing a transit gateway from a redundancy group in the console
{: #remove-redundancy-group-ui}
{: ui}

Transit gateways cannot be moved between redundancy groups.

To remove a transit gateway from a redundancy group, you must delete the transit gateway and then recreate it with a different redundancy group or without a redundancy group.

To remove a transit gateway from a redundancy group in the UI, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**.
1. Select the transit gateway that you want to remove from the redundancy group.
1. Delete the transit gateway.
1. (Optional) Create a new transit gateway without a redundancy group or with a different redundancy group.

If the deleted transit gateway is the last member of the redundancy group, the redundancy group is also deleted.
{: note}

## Removing a transit gateway from a redundancy group from the CLI
{: #remove-redundancy-group-cli}
{: cli}

Transit gateways cannot be moved between redundancy groups. To remove one, delete it and recreate it with a different redundancy group or without one.

Delete the transit gateway:

```sh
ibmcloud tg gateway-delete GATEWAY_ID
```
{: pre}

Recreate the transit gateway without a redundancy group:

```sh
ibmcloud tg gateway-create --name NAME --location LOCATION \
  --routing global
```
{: pre}

Or create a transit gateway with a different redundancy group:

```sh
ibmcloud tg gateway-create --name NAME --location LOCATION \
  --routing global \
  --redundancy-group NEW_GROUP_NAME
```
{: pre}

## Removing a transit gateway from a redundancy group with the API
{: #remove-redundancy-group-api}
{: api}

Transit gateways cannot be moved between redundancy groups. To remove one, delete it and recreate it with a different redundancy group or without one.

Delete the transit gateway:

```sh
DELETE /transit_gateways/{id}
```
{: pre}

Create a new transit gateway without a redundancy group:

```sh
POST /transit_gateways

{
  "name": "example-tg",
  "location": "us-south",
  "global": true
}
```
{: pre}

Or create a transit gateway with a different redundancy group:

```sh
POST /transit_gateways

{
  "name": "example-tg",
  "location": "us-south",
  "global": true,
  "redundancy_group": "new-group"
}
```
{: pre}

If the deleted transit gateway is the last member of the redundancy group, the redundancy group is also deleted.
{: note}

## Removing a transit gateway from a redundancy group with Terraform
{: #remove-redundancy-group-terraform}
{: terraform}

Transit gateways cannot be moved between redundancy groups. To remove one, destroy the resource and recreate it with a different redundancy group or without one.

Destroy the existing transit gateway:

```sh
terraform destroy
```
{: pre}

Update your configuration to remove or change the `redundancy_group` attribute:

```terraform
resource "ibm_tg_gateway" "example" {
  name     = "transit-gateway-1"
  location = "us-south"
  global   = true
}
```
{: codeblock}

Apply the updated configuration:

```sh
terraform apply
```
{: pre}

If the last transit gateway in a redundancy group is removed, the redundancy group is also deleted.
{: note}

## Next steps
{: #redundancy-groups-related}

- Review [Redundancy group considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#redundancy-groups-tips) to understand routing behavior, ECMP interaction, and GRE propagation across gateways in the group before making configuration changes in production.
- If you need to add connections to the transit gateways in the group, see [Creating a transit gateway](/docs/transit-gateway?topic=transit-gateway-ordering-transit-gateway) to provision a new gateway or [Changing transit gateway configuration](/docs/transit-gateway?topic=transit-gateway-change-configuration) to update an existing one. Remember that connections must be added to each gateway in the redundancy group independently to achieve full redundancy.
- To verify that routes are flowing correctly across the gateways, [generate a route report](/docs/transit-gateway?topic=transit-gateway-route-reports) and check for expected prefixes on each transit gateway.
