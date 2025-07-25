---

copyright:
  years: 2020, 2025
lastupdated: "2025-07-25"

keywords: features, overview

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Adding a connection
{: #adding-connections}

You can add a connection to a transit gateway by using the UI, CLI, API, and Terraform.
{: shortdesc}

## Adding a connection in the UI
{: #tg-ui-adding-connection-transit-gateway}
{: ui}

To add a connection to a transit gateway, follow these steps:
1. Open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**.
1. Click the name of the transit gateway where you want to add a connection.

   If you are in the expanded view, click **View full details**.
   {: tip}

1. In the Connections view, click **Add connection**.
1. Choose and configure the specific network connections that you want to add to your transit gateway. Choices include:

   * **Classic infrastructure** - Allows you to connect to IBM Cloud classic resources.
   * **Direct Link** - Creates a network connection to and from Direct Link gateways so that there is a secure connection to on-premises networks and other resources that are connected to the transit gateway.

      If you select **Direct Link**, you must also log in to the [Direct Link console](/interconnectivity/direct-link){: external} (that uses the same IBM Cloud account) and specify **Transit Gateway** as the type of network connection for your direct link.
      {: important}

   * **{{site.data.keyword.powerSys_notm}}** - Creates a network connection to and from a {{site.data.keyword.powerSys_notm}} instance so that there is a secure connection to networks and other resources connected to the transit gateway.

      Location: Select a region for the {{site.data.keyword.powerSys_notm}} workspace.

      If you select **{{site.data.keyword.powerSys_notm}}**, you must have a {{site.data.keyword.powerSys_notm}} workspace created in a PER-enabled data center.For a list of PER-enabled data centers, see [Getting started with the Power Edge Router](/docs/power-iaas?topic=power-iaas-per).

      To find out if your {{site.data.keyword.powerSys_notm}} workspace is set up correctly, go to the workspace and check the navigation for a Cloud connections page. If there isn't a **Cloud connections** page, the workspace leverages the Power Edge Router and can be added as a connection to Transit Gateway. Otherwise, you must configure virtual connections with Cloud connections on the {{site.data.keyword.powerSys_notm}}.
      {: important}

   * **Redundant GRE** allows unbound GRE tunnels to connect to endpoints in either VPC or classic infrastructure networks, thus allowing you to build in redundancy for GRE tunnels. For more information, see [Creating a redundant GRE tunnel](/docs/transit-gateway?topic=transit-gateway-redundant-gre-connection).

   * **Unbound GRE tunnel** - Allows a transit gateway to connect to overlay networks hosted on classic infrastructure resources. For prerequisites and detailed instructions, see [Creating an unbound GRE tunnel](/docs/transit-gateway?topic=transit-gateway-unbound-gre-connection).

   * **VPC** - Allows you to connect to your account's VPC resources, or VPC resources from other accounts as well.

1. Click **Add** to create a connection.

## Adding a connection from the CLI
{: #tg-cli-adding-connection-transit-gateway}
{: cli}

### Before you begin
{: #cli-prereqs-before-you-begin}

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

To add a connection on the transit gateway from the CLI, enter the following command:

```sh
ibmcloud tg connection-create|cc GATEWAY_ID --name NAME --network-type [vpc | directlink | classic] --network-id NETWORK_ID --network-account-id NETWORK-ACCOUNT-ID [--output json] [-h, --help]
```
{: pre}

Where:

- **GATEWAY_ID**: ID of the gateway that the new connection will be on.
- **--name**: Name for the new connection.
- **--network-type**: Network type of the connection. Values are `classic`, `directlink`, `power_virtual_server`, and `vpc`.
- **--network-id**: ID of the network connection. For `classic`, do not set a value. Use the CRN for all other network types. For example, to find the CRN of a VPC:

   ```sh
   ibmcloud is vpc VPC_ID --json
   ```
   {: pre}

- **--network-account-id**: ID of the IBM Cloud account to use for creating a classic connection. Only used with 'classic' type, when the account of the connection is different than the gateway's account.

- **--output JSON**: Optional: Specify if you want the output to display in JSON format.

- **--help | -h**: Optional: Get help on this command.

#### Examples
{: #connection-create-examples}

This example illustrates creating a VPC connection named `vpc-connection` using `vpcCRN="crn:v1:bluemix:public:is:us-south:a/3aa0a9999a1a46258064d84f7f447920::vpc:r134-f87014d5-87d2-46d1-9999-24683082f6bc"`:

```sh
ibmcloud tg cc $gateway --name vpc-connection --network-id $vpcCRN --network-type vpc
```
{: pre}

Create Classic connection named `classic-conn`.

```sh
ibmcloud tg cc $gateway --name classic-conn --network-type classic
```
{: pre}

## Adding a connection with the API
{: #tg-api-adding-connection-transit-gateway}
{: api}

To add a connection with the API, follow these steps:

1. Set up your [API environment](/docs/vpc?topic=vpc-set-up-environment&interface=api#api-prerequisites-setup).
1. Store any additional variables to be used in the API commands.
1. Add a connection to the transit gateway. For example:

   ```sh
   curl -X POST --location --header "Authorization: Bearer {iam_token}" \
     --header "Accept: application/json" \
     --header "Content-Type: application/json" \
     --data '{ "network_type": "vpc" }'
     "
   {base_url}/transit_gateways/{transit_gateway_id}/connections?version={version}"
   ```
   {: pre}

For more information, see [Adds a connection to a Transit Gateway](/apidocs/transit-gateway?code=java#create-transit-gateway-connection) in the Transit Gateway API reference.
{: note}

## Adding a connection by using Terraform
{: #tg-terraform-adding-connection-transit-gateway}
{: terraform}

Review the following argument references that you can specify for your resource when you create a connection for a transit gateway using Terraform:

|Argument|Details|
|--|--|
|**base_connection_id**  \n Optional  \n Forces new resource \n string | The ID of a network_type 'classic' connection a tunnel is configured over.  \n This field only applies to network type `gre_tunnel` connections.|
|**base_network_type**  \n Optional  \n Forces new resource  \n string | The base network type. Allowed values are `classic`.  \n This field only applies to `unbound_gre_tunnel` type connections.
|**gateway**  \n Required  \n Forces new resource  \n string | Enter the transit gateway identifier.|
|**local_gateway_ip**  \n Optional  \n Forces new resource  \n string | The local gateway IP address. \n This field is required for, and only applicable to, `gre_tunnel` and `unbound_gre_tunnel` type connections. |
|**local_tunnel_ip**  \n Optional  \n Forces new resource  \n string | The local tunnel IP address. \n This field is required for, and only applicable to, `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**name**  \n Optional  \n string | The connection name. If the name is not given, a default name is provided based on the network type, such as `vpc` for network type VPC and `classic` for network type classic.|
|**network_account_id**  \n Optional  \n Forces new resource  \n string|The ID of the network connected account. This is used if the network is in a different account than the gateway.|
|**network_type**  \n Required  \n Forces new resource  \n string | The network type. Allowed values are `classic`, `directlink`, `gre_tunnel`, `unbound_gre_tunnel`, and `vpc`. |
|**network_id**  \n Optional  \n Forces new resource  \n string | The ID of the network that is being connected to through this connection. \n This parameter is required for network type `vpc` and `directlink`, the CRN of the VPC or direct link gateway to be connected.  \n This field is required to be unspecified for network type `classic`.  \n **Example**:`crn:v1:bluemix:public:is:us-south:a/123456::vpc:4727d842-f94f-4a2d-824a-9bc9b02c523b`|
|**remote_bgp_asn**  \n Optional  \n Forces new resource  \n integer | The remote network BGP ASN (will be generated for the connection if not specified).  \n This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**remote_gateway_ip**  \n Optional  \n Forces new resource  \n string | The remote gateway IP address. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**remote_tunnel_ip**  \n Optional  \n Forces new resource  \n string | The remote tunnel IP address. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**zone**  \n Optional  \n Forces new resource  \n string | The location of the GRE tunnel. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections. |
{: caption="Terraform argument references for creating a connection" caption-side="bottom"}

### Example
{: #tg-terraform-adding-connection-transit-gateway-example}

This example illustrates creating a transit gateway connection that uses Terraform:

```sh
resource "ibm_tg_connection" "test_ibm_tg_connection" {
  gateway      = ibm_tg_gateway.test_tg_gateway.id
  network_type = "vpc"
  name         = "myconnection"
  network_id   = ibm_is_vpc.test_tg_vpc.resource_crn
}
```
{: pre}
