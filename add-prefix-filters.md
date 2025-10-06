---

copyright:
  years: 2020, 2025
lastupdated: "2025-10-06"

keywords:

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Adding and deleting prefix filters
{: #adding-prefix-filters}

With prefix filtering, you can set an ordered list of prefix route filters for a transit gateway connection.
{: shortdesc}

## Before you begin
{: #adding-prefix-filters-begin}

Make sure to review [Prefix filtering considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips&interface=ui#prefix-filtering-considerations) before you add or delete a prefix filter.

## Adding prefix filters to an existing connection in the UI
{: #adding-prefix-filters-ui-new-existing}
{: ui}

To add prefix filtering to an existing connection in the UI, follow these steps:

1. From the Transit Gateway page, click the name of the gateway where you want to add prefix filters.
1. The prefix filtering icon ![Prefix filter icon](/images/prefix-filter-icon.png) shows if a connection already has prefix filters. Click **View** next to **Prefix filters** to show the prefix filter list.

    To modify an existing prefix filter, click the Actions menu ![Actions menu](../../icons/action-menu-icon.svg) and select **Prefix filtering**.
    {: tip}

1. If the connection does not have existing prefix filters, click the Actions menu ![Actions menu](../../icons/action-menu-icon.svg) and select **Prefix filtering**.
1. Adjust the default filter as needed. Your choices are as follows:

    * **Permit prefixes** (default) indicates that all prefixes in this connection are accessible to all other connections in this transit gateway. In this case, "all" means up to the established quota and limits.
    * **Deny prefixes** indicates that no prefixes from this connection are accessible to any other connection on this transit gateway.

1. Click **Create prefix filter**, then configure the filter with the following options:

    * Select an action.
    * Enter the network prefix along with the subnet mask.
    * Optionally, enter values if the network should be greater than or equal to a wanted subnet mask.
    * Adjust the order of the filters in the routing table as needed, then click **Save**.

## Deleting prefix filters in the UI
{: #deleting-prefix-filters-ui}
{: ui}

To delete a prefix filter for an existing connection in the UI, follow these steps:

1. From the details page of the transit gateway, identify the connection where you want to delete prefix filters.

   The prefix filtering icon ![Prefix filter icon](/images/prefix-filter-icon.png) shows if a connection already has prefix filters.
1. Click the connection's Actions menu ![Actions menu icon](../../icons/action-menu-icon.svg) and select **Prefix filtering**.
1. Click the Actions menu ![Actions menu icon](../../icons/action-menu-icon.svg) next to the prefix filter that you want to delete. Then, click **Delete**.
1. Click **Delete prefix filter** to confirm deletion.

## Adding prefix filters from the CLI
{: #adding-prefix-filters-cli}
{: cli}

To add prefix filters from the CLI, follow these steps:

```sh
ibmcloud tg prefix-filter-create GATEWAY_ID CONNECTION_ID --prefix PREFIX --action ACTION [--le LE] [--ge GE] [--before BEFORE] [--output json]
```
{: pre}

Where:

- **GATEWAY_ID**: ID of the gateway that the prefix filter is being applied to.

- **CONNECTION_ID**: ID of the connection that the prefix filter is being applied to.

- **--prefix**: Network prefix that the filter will be applied to.

- **--action**: Action to take on the specified prefix (`permit` | `deny`).

- **--le**: Optional: The prefix filter is applied to a subnet mask less than or equal to this value.

- **--ge**: Optional: The prefix filter is applied to a subnet mask greater than or equal to this value.

- **--before**: Optional: Identifier of the prefix filter that this filter should be applied before. If empty, this filter is applied last.

- **--output**: Optional: Specify whether you want the output to display in JSON format.
 
### Example: Creating a prefix filter
{: #adding-prefix-filters-cli-example}

An example of creating a prefix filter from the CLI is as follows:

```sh
ibmcloud tg pfc 9f559c43-63f4-4da5-b312-b525a8dce185 6c1bdc19-4adb-4760-8cdc-ef3b74b626f7 --prefix 10.0.250.0/24 --action permit --le 32 --ge 28

FilterID   b4dbe0a6-c52d-4128-cc32-6f53d86bc82b
Prefix     10.0.250.0/24
Action     permit
Ge         28
Le         32
Before
Created    2022-02-28T12:35:09.226-06:00
Updated    2022-02-28T12:35:09.226-06:00
```
{: pre}

## Deleting prefix filters from the CLI
{: #deleting-prefix-filters-cli}
{: cli}

To delete prefix filters from the CLI, follow these steps:

```sh
ibmcloud tg prefix-filter-delete GATEWAY_ID CONNECTION_ID FILTER_ID [-f, --force]
```
{: pre}

Where:

- **GATEWAY_ID**: ID of the gateway that the prefix filter will be deleted from.

- **CONNECTION_ID**: ID of the connection that the prefix filter will be deleted from.

- **FILTER_ID**: ID of the prefix filter that is being deleted.

- **--force, -f**: Force the deletion operation without confirmation.

### Example: Deleting a prefix filter
{: #deleting-prefix-filters-cli-example}

This is an example of deleting a prefix filter from the CLI.

```sh
ibmcloud tg pfd 9f559c43-63f4-4da5-b312-b525a8dce185 6c1bdc19-4adb-4760-8cdc-ef3b74b626f7 b4dbe0a6-c52d-4128-cc32-6f53d86bc82b

This deletes filter b4dbe0a6-c52d-4128-cc32-6f53d86bc82b on gateway 9f559c43-63f4-4da5-b312-b525a8dce185 connection 6c1bdc19-4adb-4760-8cdc-ef3b74b626f7 and can't be undone. Continue [y/N] ?> Y
Deleting filter b4dbe0a6-c52d-4128-cc32-6f53d86bc82b on gateway 9f559c43-63f4-4da5-b312-b525a8dce185 connection 6c1bdc19-4adb-4760-8cdc-ef3b74b626f7 under account bbstsdv1 - IBM as user Hasan.Mahmood.Khan@ibm.com...
OK
Filter b4dbe0a6-c52d-4128-cc32-6f53d86bc82b is deleted.
```
{: pre}

## Adding prefix filters with the API
{: #adding-prefix-filters-api}
{: api}

Follow these steps to add a prefix filter to a connection with the API:

1. Set up your [API environment](/docs/vpc?topic=vpc-set-up-environment&interface=api#api-prerequisites-setup).
1. Store any additional variables to be used in the API commands.
1. When all variables are initiated, add prefix filters. For example:

   ```sh
   curl -X POST --location --header "Authorization: Bearer
   {iam_token}" \
   --header "Accept: application/json" \
   --header "Content-Type: application/json" \
   --data '{ "location": "us-south", "name": "Transit_Service_BWTN_SJ_DL" }' \
   "{base_url}/transit_gateways?version={version}"
   ```
   {: pre}

For more information, see [Adds a prefix filter to a Transit Gateway Connection](/apidocs/transit-gateway#create-transit-gateway-connection-prefix-filter) in the Transit Gateway API reference.
{: note}

## Deleting prefix filters with the API
{: #deleting-prefix-filters-api}

1. Set up your [API environment](/docs/vpc?topic=vpc-set-up-environment&interface=api#api-prerequisites-setup).
1. Store any additional variables to be used in the API commands.
1. When all variables are initiated, add prefix filters. For example:

   ```sh
   curl -X DELETE --location \
   --header "Authorization: Bearer {iam_token}" \
   "{base_url}/transit_gateways/{transit_gateway_id}/connections/{id}/prefix_filters/{filter_id}?version={version}"
   ```
   {: pre}

For more information, see [Removes a prefix filter from Transit Gateway Connection](/apidocs/transit-gateway#delete-transit-gateway-connection-prefix-filter) in the Transit Gateway API reference.
{: note}

## Adding and deleting prefix filters with Terraform
{: #working-prefix-filters-terraform}
{: terraform}

Review the following argument references that you can specify for your resource when you add or delete a prefix filter:

|Argument|Details|
|--|--|
|**gateway**  \n Required \n String | The unique identifier of the gateway. |
|**connection_id**  \n Required  \n String | The unique identifier of the gateway connection.|
|**action**  \n Required  \n String | Whether to permit or deny any matching prefix. |
|**prefix**  \n Required  \n String | The IP prefix. |
|**before**  \n Optional  \n String | The identifier of the prefix filter to place this filter in front of. When a filter references another filter in it's `before` field, then the filter making the reference is applied before the referenced filter.  \n For example, if filter A references filter B in its `before` field, A is applied before B. |
|**ge**  \n Optional  \n Integer | The IP prefix GE. The GE (greater than or equal to) value sets the minimum prefix length on which the filter action is applied. |
|**le**  \n Optional  \n Integer | The IP prefix LE. The LE (less than or equal to) value sets the maximum prefix length on which the filter action is applied. |
{: caption="Arguments when adding or deleting a prefix filter using Terraform" caption-side="bottom"}

### Example
{: #working-prefix-filters-terraform-example}

This example shows how to add a prefix filter:

``` sh
resource "ibm_tg_connection_prefix_filter" "test_tg_prefix_filter" {
    gateway = ibm_tg_gateway.new_tg_gw.id
    connection_id = ibm_tg_connection.test_ibm_tg_connection.connection_id
    action = "permit"
    prefix = "192.168.100.0/24"
    le = 32
    ge = 24
}
```
{: codeblock}

To remove a prefix filter, use the `terraform destroy -target=ibm_tg_connection_prefix_filter.[prefix filter name]` command.
{: tip}
