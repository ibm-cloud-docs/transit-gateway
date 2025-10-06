---

copyright:
  years: 2020, 2025
lastupdated: "2025-10-06"

keywords: connecting, region, order

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Creating a transit gateway
{: #ordering-transit-gateway}
{: help}
{: support}

To order IBM Cloud Transit Gateway, you must determine the location connecting to IBM Cloud, complete the required configuration information, and then submit your order.

## Creating a transit gateway in the UI
{: #tg-ui-creating-transit-gateway}
{: ui}

To get started using {{site.data.keyword.tg_full_notm}}, follow these steps:
{: shortdesc}

1. Review requirements and configuration considerations in [Planning for Transit Gateway](/docs/transit-gateway?topic=transit-gateway-helpful-tips).
1. From your browser, open the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog){: external} and log in to your account.
1. Select **Networking** in the navigation pane, then click the Transit Gateway tile. The Transit Gateway ordering page displays.

   You can also access the ordering page from the [{{site.data.keyword.cloud_notm}} console](/login){: external} by selecting the Navigation Menu icon ![Menu icon](../../icons/icon_hamburger.svg) on the upper left of the page. Then, click **Infrastructure** > **Network** > **Transit Gateway**. Click **Create** to open the provisioning page.
   {: tip}

1. Enter a name for the transit gateway and choose a resource group. You can select a resource group from the list, or keep the **default** selection.
1. Optional: Click the **GRE enhanced route propagation** toggle to allow GRE tunnel traffic to flow across all GRE tunnels connected to this transit gateway. 

   Make sure to review [GRE enhanced propagation considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips&interface=ui#gre-enhanced-route-propagation-considerations) before enabling this toggle.
   {: note}

1. Choose a routing option:

   All of your classic resources and Direct Link connections across MZRs can be accessed regardless of whether local or global routing is enabled.
   {: remember}

   * Select **Local routing** to allow your transit gateway to connect to all VPC and classic resources within the transit gateway's provisioned region.
   * Select **Global routing** to allow your transit gateway to connect to VPC resources in all IBM [Multi-Zone Regions (MZRs)](/docs/overview?topic=overview-locations#table-mzr).

   You can upgrade routing options at a later point if your needs change. Pricing is changed accordingly.
   {: note}

1. Choose the location where you want to provision your transit gateway.

   If you are using local routing, the specified location limits you to connect VPCs located in that region only. If you are using global routing, the specified location affects network latency, so choose the region closest to the resources that you need connected.

1. Add connections to your transit gateway now, or after it has been provisioned. {: #add-connection}

   1. Select the network connection to be attached to the transit gateway. To add connections later, see [Adding a connection](/docs/transit-gateway?topic=transit-gateway-adding-connections).

      You can add a connection on the same account as the connection type, or request to connect to a network in another account.
      {: note}

      Select from the following connection types:

      * **Classic infrastructure** networks allow you to connect to IBM Cloud classic resources. Only one classic infrastructure connection is allowed per account.

      * **Direct Link** creates a network connection to and from Direct Link gateways so that there is a secure connection to on-premises networks and other resources connected to the transit gateway.

         If you select **Direct Link**, you must also log in to the [Direct Link console](/interconnectivity/direct-link){: external} and specify **Transit Gateway** as the type of network connection for your direct link.
         {: important}

      * **{{site.data.keyword.powerSys_notm}}** - Creates a network connection to a {{site.data.keyword.powerSys_notm}} workspace to access the resources in a {{site.data.keyword.powerSys_notm}} colo.

         If you select **{{site.data.keyword.powerSys_notm}}**, a {{site.data.keyword.powerSys_notm}} workspace must be created in a PER-enabled data center. For a list of PER-enabled data centers, see [Getting started with the Power Edge Router](/docs/power-iaas?topic=power-iaas-per).
         {: note}

      * **Redundant GRE** allows unbound GRE tunnels to connect to endpoints in either VPC or classic infrastructure networks, thus allowing you to build in redundancy for GRE tunnels. See [Creating a redundant GRE tunnel](/docs/transit-gateway?topic=transit-gateway-redundant-gre-connection) for further instructions.
 
      * **Unbound GRE tunnel** allows a transit gateway to connect to overlay networks hosted on classic infrastructure resources. See [Creating an unbound GRE tunnel](/docs/transit-gateway?topic=transit-gateway-unbound-gre-connection) for further instructions.

      * **VPC** networks can contain compute resources, allowing you to connect to your account's VPC resources, or, with approval, another account's VPC resources.

   1. [REVIEW]{: tag-red} Optionally, expand the Prefix filtering section to show the **Permit prefixes** toggle where you can create prefix filters. Prefix filtering allows you to set an ordered list of filters that determine the routes your transit gateway should accept or deny.   

         Make sure to review [Prefix filtering considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips&interface=ui#prefix-filtering-considerations) before creating prefix filters. Also, note that the default filter applies to all prefixes except those that you create.
      {: attention}

      To create a prefix filter, click **Create prefix filter**, then complete the following information:
    
      1. Select an action type: **Permit** or **Deny**.
      1. Enter the network prefix along with its subnet mask (for example, `10.0.0.0/16`).
      1. Optionally, enter values for whether the network should be greater than or equal to the subnet mask you chose.
      1. Click **Save** to add the prefix filter.

      Connections are denied or permitted based on the order of the filters in the list. Edit the prefix filter list to adjust the order in which prefixes are processed.
      {: tip}

   1. Complete base network information (different depending on selected network connection) and choose a connection reach option:

      * **Add new connection in this account** - Enter a connection name and any other required information for your connection.

         * For **{{site.data.keyword.powerSys_notm}}**, select a location for the {{site.data.keyword.powerSys_notm}} workspace. Then, select from the list of  {{site.data.keyword.powerSys_notm}} workspaces that are enabled for Transit Gateway. Keep in mind that not all {{site.data.keyword.powerSys_notm}} workspaces show in this menu. 

      * **Request connection to a network in another account** - Enter either the IBM Cloud ID or Cloud Resource Name (CRN) of the account that manages the network where you want to connect. Then, complete any remaining information. All resources connected to that transit gateway will be accessible from the other network. For more information, including how to obtain the Cloud ID or CRN, see [Adding a cross-account connection](/docs/transit-gateway?topic=transit-gateway-adding-cross-account-connections&interface=ui).

         * IBM Cloud ID - Required by **Classic infrastructure** and **Unbound GRE tunnel**.
         * CRN - Required by all other connections.

         To find out if your Power Systems Virtual Server workspace is set up correctly, go to the Power Systems Virtual Server UI and check the navigation for a Cloud connections page. If there isn't a Cloud connections page, the workspace leverages Transit Gateway. Otherwise, you must configure virtual connections with Cloud connections on the Power Systems Virtual Server.
         {: important}
 
1. Click **Create** to complete your order.

## Creating a transit gateway from the CLI
{: #tg-cli-creating-transit-gateway}
{: cli}

Before you begin, complete these prerequisites to use the Transit Gateway CLI, which is implemented as an {{site.data.keyword.cloud_notm}} CLI plug-in.

1. Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli#install-ibmcloud-cli){: external}.
1. Install the `tg-cli/tg` CLI plug-in to the {{site.data.keyword.cloud_notm}} CLI.

   To install:

   ```sh
   ibmcloud plugin install tg
   ```
   {: pre}

If you are going to use the CLI with a Virtual Private Endpoint (VPE), you must set the following variable:

```sh
export IBMCLOUD_TG_API_ENDPOINT=private.transit.cloud.ibm.com
```
   {: pre}

To create a transit gateway from the CLI, enter the following command:

```sh
ibmcloud tg gateway-create|gwc --name NAME --location LOCATION [--routing ROUTING] [--gre-enhanced-route-propagation true | false] [--resource-group-id RES_GROUP_ID] [--output json] [-h, --help]
```
{: pre}

Where:

- **--name** - Name for the new gateway.
- **--location** - Location of the gateway (see possible values by using : `ibmcloud tg locations`)
- **--routing** - Gateway routing of resources (`global` | `local`). Use `global` to connect resources across regions. The default value is `local`.
- **--resource-group-id** - Optional: Gateway resource group ID. Uses the default resource group, if not specified.
- **--gre-enhanced-route-propagation** - Optional: Specify if you want to enable route propagation across all GREs connected to the same transit gateway. One of: `true` or `false` (default).
- **--output json** - Optional: Specify to display the output in JSON format.
- **--help | -h** - Optional: Get help on this command.

### Example
{: #tgw-create-examples}

The following example illustrates creating a gateway named `myGateway` in us-south with local routing and using the default resource group:

```sh
ibmcloud tg gwc --name myGateway --location us-south
```
{: pre}

## Creating a transit gateway using the API
{: #tg-api-creating-transit-gateway}
{: api}

Follow these steps to create a transit gateway with the API:

1. Set up your [API environment](/docs/vpc?topic=vpc-set-up-environment&interface=api#api-prerequisites-setup).
1. Store any additional variables to be used in the API commands.
1. When all variables are initiated, create the transit gateway:

   ```sh
   curl -X POST --location --header "Authorization: Bearer
   {iam_token}" \
   --header "Accept: application/json" \
   --header "Content-Type: application/json" \
   --data '{ "location": "us-south", "name": "Transit_Service_BWTN_SJ_DL" }' \
   "{base_url}/transit_gateways?version={version}"
   ```
   {: pre}

For more information, see [Creates a Transit Gateway](/apidocs/transit-gateway?code=java#create-transit-gateway) in the Transit Gateway API reference.
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
|**gre_enhanced_route_propagation** \n  Optional \n boolean | Specify if you want to enable route propagation across all GREs connected to the same transit gateway. |
|**resource_group**  \n Optional  \n Forces new resource  \n string | The resource group ID where the transit gateway is to be created.|
{: caption="Argument references for creating a transit gateway" caption-side="bottom"}

### Example
{: #tg-terraform-creating-transit-gateway-example}

This example illustrates creating a transit gateway in Terraform:

```sh
resource "ibm_tg_gateway" "new_tg_gw"{
name="transit-gateway-1"
location="us-south"
global=true
gre_enhanced_route_propagation=false
resource_group="30951d2dff914dafb26455a88c0c0092"
}
```
{: screen}
