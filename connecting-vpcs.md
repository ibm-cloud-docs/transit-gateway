---

copyright:
  years: 2020, 2022
lastupdated: "2022-02-24"

keywords: connecting, vpc, region, order

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Ordering IBM Cloud Transit Gateway
{: #ordering-transit-gateway}
{: help}
{: support}

## Creating a transit gateway using the UI
{: #tg-ui-creating-transit-gateway}
{: ui}

To get started using {{site.data.keyword.tg_full_notm}}, follow these steps:
{: shortdesc}

1. Review requirements and configuration considerations in [Planning for Transit Gateway](/docs/transit-gateway?topic=transit-gateway-helpful-tips).
1. From your browser, open the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog){: external} and log in to your account.
1. Select **Networking** in the navigation pane, then click the Transit Gateway tile.

   You can also access the ordering page from the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com){: external} by selecting the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) on the upper left of the page. Then, select **Interconnectivity** > **Transit Gateway** and click the **Create transit gateway** button.
   {: tip}

   The Transit Gateway ordering page displays.

   ![Transit gateway ordering page](images/tg-ordering.png "Transit gateway ordering page"){: caption="Transit gateway ordering page" caption-side="bottom"}

1. Enter a name for the transit gateway and choose a resource group. You can select a resource group from the list, or keep the default selection.

1. Choose a routing option:

   * Select **Local routing** if you want your transit gateway to connect to all VPC and classic resources within the transit gateway's provisioned region.  Data transfer is free.
   * Select **Global routing** if you want your transit gateway to connect to VPC resources in all IBM [Multi-Zone Regions (MZRs)](/docs/overview?topic=overview-locations#mzr-table). Data transfer fees are changed at $0.02 per GB for data transfer above the 1 TB free monthly allotment.

   You can upgrade routing options at a later point if your needs change. Pricing is changed accordingly.
   {: note}

   Remember that all of your classic resources across MZRs can be accessed regardless of routing choice.
   {: tip}

1. Choose the location where you want to provision your transit gateway. 

   If you are using local routing, the specified location limits you to connect VPCs located in that region only. If you are using global routing, the specified location affects the price for data transfer, so choose the region closest to the resources that you need connected.

1. Add connections to your transit gateway now, or after it has been provisioned.

   * To add connections now, select the network connection to be attached to the transit gateway. To add connections later, see [Adding a connection](/docs/transit-gateway?topic=transit-gateway-edit-gateway#adding-connections). Cross account (VPC only) connections can only be added later, after you provision the gateway.

      Select from the following connection types:

      * **Classic infrastructure** networks allow you to connect to IBM Cloud classic resources. Only one classic infrastructure connection is allowed per account.
      * **VPC** networks can contain compute resources, allowing you to connect to your account's VPC resources, or, with approval, another account's VPC resources.
      * **GRE Tunnel** allows a transit gateway to connect to overlay networks hosted on classic infrastructure resources in approved use cases. For more information, see [Creating a Generic Routing Encapsulation (GRE) tunnel connection](/docs/transit-gateway?topic=transit-gateway-GRE-connection).
      * **Direct Link** creates a network connection to and from Direct Link 2.0 gateways so that there is a secure connection to on-premises networks and other resources connected to the transit gateway.

         If you select **Direct Link**, you must also log in to the [Direct Link console](https://cloud.ibm.com/interconnectivity/direct-link){: external} (using the same IBM Cloud account) and specify **Transit Gateway** as the type of network connection for your direct link. You can specify the connection type when you create a direct link, or after your direct link is provisioned. For instructions, see [Updating the network connection type](/docs/dl?topic=dl-virtual-connection-types){: external}.
         {: important}

   * After you select a network connection, choose a connection reach option:
   
      * **Add new connection in this account** - Enter an optional connection name.
      * **Request connection to a network in another account** - Enter the IBM Cloud ID of the account that manages the network that you want to connect to, and a connection name. All resources connected to that transit gateway will be accessible from the other network.   

   * Complete all other required information for your connection.
  
1. Optionally, you can create prefix filters to permit or deny specific routes on specific connections. 
   
   For prefix filtering considerations and step-by-step instructions, see [Adding and deleting prefix filters](docs/transit-gateway?topic=transit-gateway-adding-prefix-filters).
   {: important}
 
   To begin, expand the drop-down arrow and complete the following information: 

   * Select the default filter that you want to use. You can either permit or deny all prefixes. 
   
      The default filter is applied only if you don't create prefix filters that bypass this default setting.
      {: note}

   * Click **New prefix filter** to start creating prefix filters. In turn, your prefix filters are added to an ordered list that is processed sequentially.
      
      ![Create prefix filters](images/prefix-filtering.png "Create prefix filters"){: caption="Create prefix filters" caption-side="bottom"}

1. **View Terms** on the right of the page.
1. Click **Create** to complete your order.

## Creating a transit gateway using the CLI
{: #tg-cli-creating-transit-gateway}
{: cli}

### Before you begin
{: #cli-ref-prereqs}

Complete these prerequisites to use the Transit Gateway CLI, which is implemented as an {{site.data.keyword.cloud_notm}} CLI plug-in.

1. Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli#install-ibmcloud-cli){: external}.
1. Install the `tg-cli/tg` CLI plug-in to the {{site.data.keyword.cloud_notm}} CLI.

   To install:

   ```sh
   ibmcloud plugin install tg
   ```
   {: pre}

If you are going to use the CLI with a Virtual Private Endpoint (VPE), you must set the following variable:

```bash
export IBMCLOUD_TG_API_ENDPOINT=private.transit.cloud.ibm.com
```
   {: pre}
   
For more information, see [Integrating with Virtual Private Endpoint for VPC](/docs/transit-gateway?topic=transit-gateway-vpe-for-ibm-cloud-transit-gateway).
{: note}

### Creating a transit gateway using the CLI
{: #gateway-create}

To create a transit gateway using the CLI, enter the following command:

```sh
ibmcloud tg gateway-create|gwc --name NAME --location LOCATION [--routing ROUTING] [--resource-group-id RES_GROUP_ID] [--output json] [-h, --help]
```
{: pre}

Where:

- **--name** - Name for the new gateway.
- **--location** - Location of the gateway (see possible values by using : `ibmcloud tg locations`)
- **--routing** - Gateway routing of resources (global | local). Use 'global' to connect resources across regions. The default value is 'local'.
- **--resource-group-id** - Optional: Gateway resource group ID. Uses the default resource group, if not specified.
- **--output json** - Optional: Specify to display the output in JSON format.  
- **--help | -h** - Optional: Get help on this command.

### Example
{: #gateway-create-examples}

The following example illustrates creating a gateway named `myGateway` in us-south with local routing and using the default resource group:

```sh
ibmcloud tg gwc --name myGateway --location us-south
```
{: pre}

## Creating a transit gateway using the API
{: #tg-api-creating-transit-gateway}
{: api}

Follow these instructions to create a transit gateway when using the API:

1. Set up your [API environment](/docs/vpc?topic=vpc-set-up-environment#api-prerequisites-setup).
1. Store any additional variables to be used in the API commands.

### Request
{: #tg-api-creating-transit-gateway-request}

To create a transit gateway, adjust the following parameters:

|Query parameters|Information|
|--|--|
| **version**  \n Required  \n string | Requests the version of the API as of a date in the format `YYYY-MM-DD`. Any date up to the current date may be provided. Specify the current date to request the latest version.  \n **Possible values:** Value must match regular expression  `^[0-9]{4}-[0-9]{2}-[0-9]{2}$`
|**Request Body**  \n Required  \n TGCreateTemplate |The Transit Gateway Template|
|**location**  \n Required  \n string|Location of Transit Gateway Services  \n **Example:** `us-south`|
|**name**  \n Required  \n Name | Name Transit Gateway Services  \n **Possible values:** 1 ≤ length ≤ 63, Value must match regular expression  `^([a-zA-Z]|[a-zA-Z][-_a-zA-Z0-9]*[a-zA-Z0-9])$`  \n **Example:** `Transit_Service_BWTN_SJ_DL`|
|**global**  \n boolean | Allow global routing for a transit gateway. If unspecified, the default value is `false`.  \n **Default:** `false`  \n **Example:** `true`|
|**resource_group**  \n ResourceGroupIdentity | The resource group to use. If unspecified, the account’s [default resource group](https://console.bluemix.net/apidocs/resource-manager#introduction) is used.|
|**id**  \n Required  \n string | The unique identifier for this resource group  \n **Possible values:** Value must match regular expression  `^[0-9a-f]{32}$`  \n **Example:** `56969d6043e9465c883cb9f7363e78e8`|
{: caption="Table 1. Parameters for creating a transit gateway" caption-side="bottom"}

#### Example Request
{: #tg-api-creating-transit-gateway-request-example}

This example illustrates creating a transit gateway using the API:

```sh
curl -X POST --location --header "Authorization: Bearer 
{iam_token}" \
--header "Accept: application/json" \
--header "Content-Type: application/json" \
--data '{ "location": "us-south", "name": "Transit_Service_BWTN_SJ_DL" }' \
"{base_url}/transit_gateways?version={version}"
```
{: pre}

### Response
{: #tg-api-creating-transit-gateway-response}

The following response shows once you initiate the request:

|Response Body |Details|
|--|--|
|**id**  \n Always included  \n ID|The unique identifier for this transit gateway  \n **Example:** `ef4dcb1a-fee4-41c7-9e11-9cd99e65c1f4`|
|**crn**  \n Always included  \n CRN|The CRN for this transit gateway  \n **Example:** `crn:v1:bluemix:public:transit:dal03:a/57a7d05f36894e3cb9b46a43556d903e::gateway:ef4dcb1a-fee4-41c7-9e11-9cd99e65c1f4`|
|**name**  \n Always included  \n string|A human readable name for the transit gateway  \n **Possible values:** 1 ≤ length ≤ 63, Value must match regular expression  `^([a-zA-Z]|[a-zA-Z][-_a-zA-Z0-9]*[a-zA-Z0-9])$`  \n **Example:** `my-transit-gateway-in-TransitGateway`|
|**location**  \n Always included  \n string|Location of the transit gateway \n **Example:** `us-south`|
|**created_at**  \n Always included  \n boolean|Allow global routing for a transit gateway  \n **Example:** `true`|
|**status**  \n Always included  \n string|The status of the transit gateway. The list of enumerated values for this property may expand in the future. Code and processes using this field must tolerate unexpected values.  \n **Possible values:** [`available`,`failed`,`pending`,`deleting`]|
|**resource_group**  \n ResourceGroupReference  \n |The resource group to use. If unspecified, the account's [default resource group](https://console.bluemix.net/apidocs/resource-manager#introduction) is used.
|- **id**  \n Always included  \n string|The unique identifier for this resource group  \n **Possible values:** Value must match regular expression  `^[0-9a-f]{32}$`  \n **Example:** `56969d6043e9465c883cb9f7363e78e8`|
|- **href**  \n Always included*  \n URL|The URL for this resource group  \n **Possible values:** Value must match regular expression  `^http(s)?:\/\/([^\/?#]*)([^?#]*)(\?([^#]*))?(#(.*))?$`  \n **Example:** `https://resource-manager.bluemix.net/v1/resource_groups/56969d6043e9465c883cb9f7363e78e8`|
|**updated_at**  \n date-time | The date and time that this gateway was last updated.|
{: caption="Table 2. Initiate response example" caption-side="bottom"}

|Status Code||
|--|--|
|**201**|The transit gateway was created successfully.|
|**400**|  An invalid transit gateway template was provided.|
|**404**|A transit gateway location could not be found for the identifier given in the template, a resource group could not be found for the given resource group identifier, or the default resource group could not be found for the account (if no resource group identifier was supplied).|
|**409**| The transit gateway could not be created as a transit gateway with the same name already exists.|
{: caption="Table 3. Status codes" caption-side="bottom"}

#### Example Response
{: #tg-api-creating-transit-gateway-response-example}

This example response illustrates that the transit gateway was created sueccessfully:

```sh
{
  "created_at": "2020-03-31T12:08:05Z",
  "crn": "crn:[...]",
  "global": true,
  "id": "ef4dcb1a-fee4-41c7-9e11-9cd99e65c1f4",
  "location": "us-south",
  "name": "example-gateway",
  "resource_group": {
    "id": "56969d6043e9465c883cb9f7363e78e8"
  },
  "status": "pending",
  "updated_at": "2020-03-31T12:08:05Z"
}
```
{: screen}

For more information (including Java, Node, Python and Go examples), see "Creates a Transit Gateway" in the [Transit Gateway API reference](apidocs/transit-gateway?code=java#create-transit-gateway).
{: note}

## Creating a transit gateway using Terraform
{: #tg-terraform-creating-transit-gateway}
{: terraform}

Review the following argument references that you can specify for your resource when creating a transit gateway using Terraform:

|Argument|Details|
|--|--|
|**location**  \n Optional  \n Forces new resource  \n integer| The location of the transit gateway.  \n **Example**: `us-south`|
|**name**  \n Required  \n string| The unique user-defined name for the gateway.  \n **Example**: `myGateway`|
|**global**  \n Required  \n boolean | The gateways with global routing (true) are able to connect to networks outside their associated region.|
|**resource_group**  \n Optional  \n Forces new resource  \n string | The resource group ID where the transit gateway is to be created.|
{: caption="Table 4. Argument references for creating a transit gateway" caption-side="bottom"}

### Example
{: #tg-terraform-creating-transit-gateway-example}

This example illustrates creating a transit gateway in Terraform:

```sh
resource "ibm_tg_gateway" "new_tg_gw"{
name="transit-gateway-1"
location="us-south"
global=true
resource_group="30951d2dff914dafb26455a88c0c0092"
} 
```
{: screen}
