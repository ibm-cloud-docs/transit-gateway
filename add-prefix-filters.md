---

copyright:
  years: 2022, 2024
lastupdated: "2024-01-22"

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

Make sure that you review the following considerations before you create a prefix filter:

* Only users in the account that contains the network can filter prefixes of that network.
* You cannot filter incoming prefixes from another account.
* Prefix filters in the list are processed sequentially. You can modify the order at any time.
* Review the [prefix service limits](/docs/transit-gateway?topic=transit-gateway-helpful-tips#service-limits) for transit gateways.
* For cross-account connections, only the account owner of the respective connection can modify prefix filters. Other accounts can view the connection, but cannot modify the filters.
* GRE tunnel configurations are not implemented as connections. Instead, their routes are learned directly on BGP sessions that are established over the tunnel. For this reason, prefix filtering is not enabled for these connections.
* If you select **Request connection to a network in another account** as the connect reach option, you cannot set prefix filters because you are not the network owner of the connection. Set the prefix filter on the account that owns the connection.
* Prefix filter subnet masks are specific. For example, a rule that is defined as `10.10.20.0/24` does not match with subnet `10.10.20.0/28` or any other subnet prefix.

## Working with prefix filters in the UI
{: #adding-prefix-filters-ui}
{: ui}

You can add prefix filters when you add a new connection. You can also add a filter to an existing connection, or delete them.

### Adding prefix filters to a new connection
{: #adding-prefix-filters-ui-new}

To add a prefix filter to a new connection in the UI, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Interconnectivity** > **Transit Gateway**.
1. From the Transit Gateway page, click the name of the gateway where you want to add prefix filters.
1. From the gateway's details page, click **Add connection**.
1. Enter the following information:

   Review requirements and configuration considerations in [Planning for Transit Gateway](/docs/transit-gateway?topic=transit-gateway-helpful-tips).
   {: important}

   * Choose a network connection. You can select from the following connection types:

      * **Classic infrastructure** networks allow you to connect to IBM Cloud classic resources. Only one classic infrastructure connection is allowed per account.
      * **VPC** networks can contain compute resources, allowing you to connect to your account's VPC resources, or, with approval, another account's VPC resources.
      * **Direct Link** creates a network connection to and from Direct Link 2.0 gateways so that there is a secure connection to on-premises networks and other resources that are connected to the transit gateway.

         If you select **Direct Link**, you must also log in to the [Direct Link console](https://cloud.ibm.com/interconnectivity/direct-link){: external} (that uses the same IBM Cloud account) and specify **Transit Gateway** as the type of network connection for your direct link. You can specify the connection type when you create a direct link, or after your direct link is provisioned. For instructions, see [Updating the network connection type](/docs/dl?topic=dl-virtual-connection-types){: external}.
         {: important}

      * **{{site.data.keyword.powerSys_notm}}** creates a network connection to and from a {{site.data.keyword.powerSys_notm}} instance so that the {{site.data.keyword.powerSys_notm}} network and resources can connect to networks and other resources that are connected to the transit gateway.

         If you select **{{site.data.keyword.powerSys_notm}}**, a Power Systems Virtual Server workspace must be created in a PER-enabled data center. For a list of PER-enabled data centers, see [Getting started with the Power Edge Router](/docs/power-iaas?topic=power-iaas-per).
         {: important}

   * For Connection reach, select one of the following options:
      * **Add new connection in this account** - Enter an optional connection name.
      * **Request connection to a network in another account** - Enter the IBM Cloud ID of the account that manages the network that you want to connect to, and a connection name. All resources connected to that transit gateway are accessible from the other network.
   * Complete all other required information for your connection.

1. Optionally, you can create prefix filters to permit or deny specific routes on specific connections.

   To begin, expand the arrow in the upper right of the Prefix filtering section. Then, complete the following information:

   * Adjust the **Default filter** as needed. Your choices are as follows:

      * **Permit prefixes** (default) accepts all prefixes after entries in the prefix filter list are processed.
      * **Deny prefixes** denies all prefixes after entries in the prefix filter list are processed.

      Regardless of the default setting, you can still permit or deny network traffic by creating prefix filters.
      {: important}

   * To create a prefix filter, select **Create prefix filter**, then complete the following information:

      * Select an action type: **Permit** or **Deny**.
      * Enter the network prefix along with its subnet mask (for example, `10.0.0.0/16`).
      * Optionally, enter values for whether the network should be greater than or equal to the subnet mask that you chose.
      * Click **Save** to add the prefix filter.

    Connections are denied or permitted based on the order of the filters in the list. Edit the prefix filter list to adjust the order in which prefixes are processed.
    {: tip}

1. On the Add connection page, click **Add** to finalize the connection using the prefix filters.

### Adding prefix filters to an existing connection
{: #adding-prefix-filters-ui-new-existing}

To add prefix filtering to an existing connection in the UI, follow these steps:

1. From the Transit Gateway page, click the name of the gateway where you want to add prefix filters.
1. The prefix filtering icon ![Prefix filter icon](images/prefix-filter-icon.png) shows if a connection already has prefix filters. Click **View** next to **Prefix filters** to show the prefix filter list.

    To modify an existing prefix filter, click the Actions menu ![Actions menu](/images/overflow.png) and select **Prefix filtering**.
    {: tip}

1. If the connection does not have existing prefix filters, click the Actions menu ![Actions menu](/images/overflow.png) and select **Prefix filtering**.
1. Adjust the default filter as needed. Your choices are as follows:

    * **Permit prefixes** (default) indicates that all prefixes in this connection are accessible to all other connections in this transit gateway. In this case, "all" means up to the established quota and limits.
    * **Deny prefixes** indicates that no prefixes from this connection are accessible to any other connection on this transit gateway.

1. Click **Create prefix filter**, then configure the filter with the following options:

    * Select an action.
    * Enter the network prefix along with the subnet mask.
    * Optionally, enter values if the network should be greater than or equal to a wanted subnet mask.
    * Adjust the order of the filters in the routing table as needed, then click **Save**.

### Deleting prefix filters
{: #deleting-prefix-filters-ui}
{: ui}

To delete a prefix filter for an existing connection in the UI, follow these steps:

1. From the details page of the transit gateway, identify the connection where you want to delete prefix filters.

   The prefix filtering icon ![Prefix filter icon](images/prefix-filter-icon.png) shows if a connection already has prefix filters.
1. Click the connection's Actions menu ![Actions menu icon](/images/overflow.png) and select **Prefix filtering**.
1. Click the Actions menu ![Actions menu icon](/images/overflow.png) next to the prefix filter that you want to delete. Then, click **Delete**.
1. Click **Delete prefix filter** to confirm deletion.

## Working with prefix filters from the CLI
{: #working-prefix-filters-cli}
{: cli}

You can add prefix filters when you add a new connection by using the CLI. You can also delete them.

### Adding prefix filters from the CLI
{: #adding-prefix-filters-cli}

To add prefix filters from the CLI, follow these steps:

```sh
ibmcloud tg prefix-filter-create GATEWAY_ID CONNECTION_ID --prefix PREFIX --action ACTION [--le LE] [--ge GE] [--before BEFORE] [--output json]
```

Where:

- **GATEWAY_ID**: ID of the gateway that the prefix filter is being applied to.

- **CONNECTION_ID**: ID of the connection that the prefix filter is being applied to.

- **--prefix**: Network prefix that the filter will be applied to.

- **--action**: Action to take on the specified prefix (`permit` | `deny`).

- **--le**: Optional: The prefix filter is applied to a subnet mask less than or equal to this value.

- **--ge**: Optional: The prefix filter is applied to a subnet mask greater than or equal to this value.

- **--before**: Optional: Identifier of the prefix filter that this filter should be applied before. If empty, this filter is applied last.

- **--output**: Optional: Specify whether you want the output to display in JSON format.

#### Example: Creating a prefix filter
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

#### Deleting prefix filters from the CLI
{: #deleting-prefix-filters-cli}
{: cli}

To delete prefix filters from the CLI, follow these steps:

```sh
ibmcloud tg prefix-filter-delete GATEWAY_ID CONNECTION_ID FILTER_ID [-f, --force]
```

Where:

- **GATEWAY_ID**: ID of the gateway that the prefix filter will be deleted from.

- **CONNECTION_ID**: ID of the connection that the prefix filter will be deleted from.

- **FILTER_ID**: ID of the prefix filter that is being deleted.

- **--force, -f**: Force the deletion operation without confirmation.

#### Example: Deleting a prefix filter
{: #deleting-prefix-filters-cli-example}

This is an example of deleting a prefix filter from the CLI.

```sh
ibmcloud tg pfd 9f559c43-63f4-4da5-b312-b525a8dce185 6c1bdc19-4adb-4760-8cdc-ef3b74b626f7 b4dbe0a6-c52d-4128-cc32-6f53d86bc82b

This deletes filter b4dbe0a6-c52d-4128-cc32-6f53d86bc82b on gateway 9f559c43-63f4-4da5-b312-b525a8dce185 connection 6c1bdc19-4adb-4760-8cdc-ef3b74b626f7 and cannot be undone. Continue [y/N] ?> Y
Deleting filter b4dbe0a6-c52d-4128-cc32-6f53d86bc82b on gateway 9f559c43-63f4-4da5-b312-b525a8dce185 connection 6c1bdc19-4adb-4760-8cdc-ef3b74b626f7 under account bbstsdv1 - IBM as user Hasan.Mahmood.Khan@ibm.com...
OK
Filter b4dbe0a6-c52d-4128-cc32-6f53d86bc82b is deleted.
```

## Working with prefix filters with the API
{: #working-prefix-filters-api}
{: api}

You can add prefix filters when you add a connection with the API. You can also delete them.

### Adding prefix filters with the API
{: #adding-prefix-filters-api}
{: api}

For more information (including Java, Node, Python and Go examples), see "Add a prefix filter to a Transit Gateway Connection" in the [Transit Gateway API reference](/apidocs/transit-gateway#create-transit-gateway-connection-prefix-filter).
{: note}

#### Example request
{: #adding-prefix-filters-api-request-example}

This example illustrates adding a prefix filter to a connection:

```sh
curl -X POST --location --header "Authorization: Bearer {iam_token}" --header "Accept: application/json" --header "Content-Type: application/json" --data '{ "action": "permit", "prefix": "192.168.100.0/24" }' "{base_url}/transit_gateways/{transit_gateway_id}/connections/{id}/prefix_filters?version={version}"

POST /transit_gateways/{transit_gateway_id}/connections/{id}/prefix_filters
```

```sh
curl -X POST "https://transit.cloud.ibm.com/v1/transit_gateways/9f559c43-63f4-4da5-b306-b525a8ddb275/connections/6c1bdc19-4adb-4550-8cdc-ef3b74b739f8/prefix_filters?version=2020-03-31" -H "Authorization: Bearer $iam_token" -H "Content-Type: application/json" -d '{"action": "deny", "prefix": "10-10.0.10/30"}'
```
 
#### Example response
{: #adding-prefix-filters-api-response-example}

This example illustrates the response that a prefix filter was added successfully:

```sh
{
  "action": "permit",
  "before": "1a15dcab-7e40-45e1-b7c5-bc690eaa9782",
  "created_at": "2021-11-15T12:08:05Z",
  "ge": 0,
  "id": "1a15dcab-7e30-45e1-b7c5-bc690eaa9865",
  "le": 32,
  "prefix": "192.168.100.0/24",
  "updated_at": "2021-11-15T12:08:05Z"
}
```

### Deleting prefix filters with the API
{: #deleting-prefix-filters-api}

For more information (including Java, Node, Python, and Go examples), see "Remove prefix filter from Transit Gateway Connection" in the [Transit Gateway API reference](/apidocs/transit-gateway#delete-transit-gateway-connection-prefix-filter).
{: note}
 
#### Example request
{: #deleting-prefix-filters-api-request-example}

This example illustrates deleting a prefix filter from a connection:

```sh
curl -X DELETE --location --header "Authorization: Bearer {iam_token}"   "{base_url}/transit_gateways/{transit_gateway_id}/connections/{id}/prefix_filters/{filter_id}?version={version}"
```

```sh
curl -X DELETE "https://transit.cloud.ibm.com/v1/transit_gateways/9f559c43-63f4-4da5-b306-b525a8ddb275/connections/6c1bdc19-4adb-4550-8cdc-ef3b74b739f8/prefix_filters/a4aad53e-5828-4ac1-8dad-a08d940772d4?version=2020-03-31" -H "Authorization: Bearer $iam_token" -H "Content-Type: application/json"
```
 
#### Example response
{: #deleting-prefix-filters-api-response-example}

This example illustrates the response that a prefix filter with the specified ID cannot be found:

```sh
{
  "errors": [
    {
      "code": "not_found",
      "message": "Cannot find Prefix Filter",
      "more_info": "https://cloud.ibm.com/apidocs/transit-gateway#error-handling"
    }
  ],
  "trace": "request_id"
}
```

## Working with prefix filters by using Terraform
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
{: caption="Table 9. Arguments when adding or deleting a prefix filter using Terraform" caption-side="bottom"}

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

To remove a prefix filter, use the `terraform destroy -target=ibm_tg_connection_prefix_filter.[prefix filter name]` command.
{: tip}
