---

copyright:
  years: 2020, 2022
lastupdated: "2022-02-14"

keywords: editing, managing, manage, edit, add, connection

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Changing your configuration
{: #change-configuration}

## Changing your configuration using the UI
{: #change-configuration-ui}
{: ui}

To change your transit gateway configuration using the UI, perform the following procedure:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Interconnectivity**.
1. Click **Transit Gateway** from the left navigation pane.
1. Click the name of the transit gateway that you want to edit.

   If you are in the expanded view, click **View details**.
   {: tip}

1. From the Connections page, click the **Actions** button at the top right, then select **Edit**.

   From here, you can change the gateway's name and its routing type (Local or Global).

   To change a transit gateway's routing type from global to local, you must delete any connections that are not local to the transit gateway's location.
   {: tip}

   When changing from Local to Global routing for a given transit gateway, you are charged for all associated connection traffic.
   {: important}

   ![Editing your configuration](images/editConnection.png "Editing your configuration"){: caption="Editing your configuration" caption-side="bottom"}

## Changing your configuration using the CLI
{: #change-configuration-cli}
{: cli}

To update properties on an existing gateway using the CLI, execute the following command:

```sh
ibmcloud tg gateway-update|gwu GATEWAY_ID [--name NAME] [--routing ROUTING] [--output json] [-h, --help]
```
{: pre}

Where:

- **GATEWAY_ID**: ID of the gateway you want to update.

- **--name**: Optional: New name of the gateway.

- **--routing**: Optional: Gateway routing of resources (global | local). Select global to connect resources across regions. Changing routing from global to local requires all existing connections to be local.

- **--output json**: Optional: Specify if you want the output displayed in JSON format.  

- **--help | -h**: Optional: Get help on this command.

### Example
{: #gateway-update-example}

This example illustrates updating a gateway with a routing value of `global`:

```sh
ibmcloud tg gwu $gateway --routing global
```
{: pre}

## Changing your configuration using the API
{: #change-configuration-api}
{: api}

You can update your transit gateway's name, global parameters, or both using the API.

### Request
{: #change-configuration-api-request}

To change the configuration on your transit gateway, set the following parameters:

| Path Parameters | Details |
|--|--|
|**id**  \n Required  \n string | The transit gateway identifier|
{: caption="Table 1. Path parameters for changing your configuration" caption-side="bottom"}

|Query parameters| Details |
|--|--|
|**version**  \n Required  \n string | Requests the version of the API as of a date in the format `YYYY-MM-DD`. Any date up to the current date may be provided. Specify the current date to request the latest version.  \n **Possible values:** Value must match regular expression  `^[0-9]{4}-[0-9]{2}-[0-9]{2}$`|
|**Request Body**  \n Required  \n TGPatchTemplate |Update a transit gateway|
|**global**  \n global|Allow global routing for a transit gateway  \n **Example**: `true`|
|**name**  \n Name|The user-defined name for this transit gateway connection.  \n **Possible values:** 1 ≤ length ≤ 63, Value must match regular expression ^([a-zA-Z]|[a-zA-Z][-_a-zA-Z0-9]*[a-zA-Z0-9])$  \n **Example:** `Transit_Service_BWTN_SJ_DL`|
{: caption="Table 2. Query parameters for changing your configuration" caption-side="bottom"}

#### Example Request
{: #change-configuration-api-request-example}

This example illustrates changing your configuration using the API:

```sh
PATCH /transit_gateways/{id}
"{base_url}/transit_gateways/{id}?version={version}"
{
  "global": true,
  "name": "my-transit-gateway"
}
```
{: pre}

### Response
{: #change-configuration-api-response}

The following response shows once you initiate the request:

|Response Body |Details|
|--|--|
|**id**  \n Always included  \n ID|The unique identifier for this transit gateway  \n **Example:** `ef4dcb1a-fee4-41c7-9e11-9cd99e65c1f4`|
|**crn**  \n Always included  \n CRN|The CRN for this transit gateway  \n **Example:** `crn:v1:bluemix:public:transit:dal03:a/57a7d05f36894e3cb9b46a43556d903e::gateway:ef4dcb1a-fee4-41c7-9e11-9cd99e65c1f4`|
|**name**  \n Always included  \n string|A human readable name for the transit gateway  \n **Possible values:** 1 ≤ length ≤ 63, Value must match regular expression  `^([a-zA-Z]|[a-zA-Z][-_a-zA-Z0-9]*[a-zA-Z0-9])$`  \n **Example:** `my-transit-gateway-in-TransitGateway`|
|**location**  \n Always included  \n string|Location of the transit gateway \n **Example:** `us-south`|
|**created_at**  \n Always included  \n date-time |The date and time that this gateway was created|
|**global**  \n Always included  \n boolean| Allow global routing for a transit gateway  \n **Example**: `true`|
|**status**  \n Always included  \n string|The status of the transit gateway. The list of enumerated values for this property may expand in the future. Code and processes using this field must tolerate unexpected values.  \n **Possible values:** [`available`,`failed`,`pending`,`deleting`]|
|**resource_group**  \n ResourceGroupReference  \n |The resource group to use. If unspecified, the account's [default resource group](https://console.bluemix.net/apidocs/resource-manager#introduction) is used.
|- **id**  \n Always included  \n string|The unique identifier for this resource group  \n **Possible values:** Value must match regular expression  `^[0-9a-f]{32}$`  \n **Example:** `56969d6043e9465c883cb9f7363e78e8`|
|- **href**  \n Always included=  \n URL|The URL for this resource group  \n **Possible values:** Value must match regular expression  `^http(s)?:\/\/([^\/?#]*)([^?#]*)(\?([^#]*))?(#(.*))?$`  \n **Example:** `https://resource-manager.bluemix.net/v1/resource_groups/56969d6043e9465c883cb9f7363e78e8`|
|**updated_at**  \n date-time | The date and time that this gateway was last updated.|
{: caption="Table 3. Initiation request response" caption-side="bottom"}

|Status code||
|--|--|
|**200**| The Transit Gateway was updated successfully.|
|**400**| The supplied Transit Gateway patch was invalid.|
|**404**| A Transit Gateway with the specified identifier could not be found.|
|**409**| The Transit Gateway could not be updated as there are pre-existing cross-region connections attached.|
{: caption="Table 4. Status codes" caption-side="bottom"}

#### Example Response
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

For more information (including Java, Node, Python and Go examples), see "Updates specified Transit Gateway" in the [Transit Gateway API reference](/apidocs/transit-gateway#update-transit-gateway).
{: note}

## Changing your configuration using the Terraform
{: #change-configuration-terraform}
{: terraform}

You can specify the following argument references for your resource when changing the configuration of your transit gateway using Terraform:

|Argument|Details|
|--|--|
|**name**  \n Required  \n Boolean | The unique user-defined name for the gateway. For example, `myGateway`|
|**global**  \n Required  \n Boolean|The gateways with global routing (true) to connect to the networks outside their associated region.|
{: caption="Table 1. Terraform argument references for changing the configuration" caption-side="bottom"}

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
