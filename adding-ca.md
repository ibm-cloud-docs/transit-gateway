---

copyright:
  years: 2020, 2025
lastupdated: "2025-11-19"

keywords:

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Adding a cross-account connection
{: #adding-cross-account-connections}

You can request connections to networks in other {{site.data.keyword.cloud_notm}} accounts, by using the UI, CLI, API, and Terraform.
{: shortdesc}

## Planning considerations
{: #tg-ca-planning}

Before you add a cross-account connection, review these considerations:

* After you connect a transit gateway to a network in another account, all resources that are connected to that transit gateway are accessible from the other network. Make sure that you use a trusted account. The following network connections are permitted as cross-account connections:

   * Classic infrastructure
   * {{site.data.keyword.dl_full_notm}}
   * {{site.data.keyword.powerSysFull}}
   * Redundant GRE
   * Unbound GRE tunnel   
   * VPC
   * VPN gateway

* Only 10 pending requests are allowed per gateway. To create more requests, you can cancel the pending connection request, or wait for it to be approved. Connection requests expire if not approved within 72 hours.
* Use of [security controls](/docs/vpc?topic=vpc-security-in-your-vpc), such as ACLs, security groups, or other network services to control traffic flow are highly recommended. IBM Cloud Transit Gateway does not provide security groups or ACLs, but the networks they attach to might and can affect transit gateway communications. For more information on ACLs and security groups, refer to the following topics:

   * [About network ACLs](/docs/vpc?topic=vpc-using-acls)
   * [Security groups versus network ACLs](/docs/vpc?topic=vpc-using-security-groups&interface=ui#security-groups-vs-network-acls)
   * [Configuring network ACLs for use with VPN](/docs/vpc?topic=vpc-configuring-acls-vpn)
   * [Configuring ACLs and security groups for use with endpoint gateways](/docs/vpc?topic=vpc-configure-acls-sgs-endpoint-gateways)

## Adding a cross-account connection in the UI
{: #tg-ui-adding-cross-account-connection-transit-gateway}
{: ui}

To connect networks that different accounts own by using the UI, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**.
1. Click the name of the transit gateway where you want to add a connection. Then, click **Add connection**.
1. Choose your network connection type. Then, select **Request connection to a network in another account**.
1. Type the CRN of the cross-account network, or if Classic infrastructure or an Unbound or Redundant GRE, enter the IBM Cloud account ID that you want to connect to.

   * To get the IBM Cloud account ID for a Classic infrastructure or an Unbound or Redundant GRE tunnel connection, select **Manage > Account** from the {{site.data.keyword.cloud_notm}} console and choose **Account Settings**. Your account ID shows in the **Account** section of the **Account settings** page.
   * To get the CRN of a VPC, VPN gateway, Direct Link, or Power Systems Virtual Server, select the Navigation Menu icon ![Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Resource list**. Expand **Networking** (for VPC and Direct Link) or **Computing** (for Power Systems Virtual Server) to list your networking resources, then locate the service that you are looking for. Next, click anywhere in the service's table row (except for the Name link). From the side window that appears, copy the CRN and paste it into the Add connection pane.

1. Complete any remaining fields, then click **Add**. The network connection now shows the **Pending** approval status in the gateway owner's account.

   For the Classic infrastructure connection, the ID number is for your IBM Cloud account, not for a SoftLayer account.
   {: note}

   The network owner's account then receives a notification of the request. If the network owner rejects the cross-account connection, no connectivity is established and the connection shows a status of **Rejected**. You can now delete this connection. If the cross-account connection is not explicitly approved, it expires after 72 hours.

   Connection requests can be resubmitted if they expire or are rejected.
   {: note}

1. A user with the [necessary IAM permissions](/docs/transit-gateway?topic=transit-gateway-iam) in the network owner's account can see the gateway and the details of all other connections that are attached to it in **View only** mode. From the network owner's account, go to the Transit Gateway page and click the gateway name in the table.

1. In the Connections section, see **Action required** to view the incoming network connection request. A user with the [necessary additional IAM permissions](/docs/transit-gateway?topic=transit-gateway-iam) can then click **Approve** to approve the request.

   After the network owner's account ensures that the connection request is from a legitimate source and approves it, the system establishes routes to and from all other networks that are connected to the same transit gateway. Use of [network ACLs and/or security groups](/docs/vpc?topic=vpc-security-in-your-vpc#security-in-your-vpc) within networks that are accessible across accounts are highly recommended to control the network traffic flows. You can unilaterally detach cross-account connections by either account through users who have the appropriate permissions.
   {: important}

   Click **Approve** to confirm. The status of the network connection indicates **Attaching**.

1. When you change back to the original account, the status of the connection changes to **Attached**, indicating that the network request was approved.

   The gateway owner's account (or the network owner's account) can delete the connection. If the network owner deletes the connection, the gateway owner sees the connection status as **Detached**.
   {: note}

## Adding a cross-account connection from the CLI
{: #tg-cli-adding-cross-account-connection-transit-gateway}
{: cli}

Creating a cross-account connection consists of the following steps:

1. Request connection to communicate with other account.
1. Approve/Reject connection on other account.

For example, to request a connection to communicate with another account, run the following command:

```sh
ibmcloud tg connection-create|cc GATEWAY_ID --name NAME --network-id NETWORK_ID --network-type NETWORK_TYPE --network-account-id ACCOUNT_ID [--zone ZONE] [--default-prefix-filter DEFAULT_PREFIX_FILTER] [--cidr CIDR] [--output json]
```
{: pre}

Where:
`GATEWAY_ID`
:   ID of the gateway that the new connection is on.

`--name`
:   Name for the new connection.

`--network-id`
:   ID of the network connection. For `classic`, don't set a value. Use the CRN for all other network types. For example, to find the CRN of a VPC:

   ```sh
   ibmcloud is vpc VPC_ID --json
   ```
   {: pre}

`--network-type`
:   Network type of the connection. Values are `classic`, `directlink`, `power_virtual_server`,`vpn_gateway`, and `vpc`.

`--network-account-id`
:   ID of the IBM Cloud account to use for creating a classic connection. Only used with `classic` type, when the account of the connection is different than the gateway's account.

`--zone`
:   Optional: Availability zone where a GRE tunnel or VPN connection will be deployed. Only applicable to the `vpn_gateway` network type.

`--default-prefix-filter`
:   Optional: Default prefix filter of the connection (`permit` | `deny`).

`--cidr`
:   Optional: CIDR block to use for the connection. Only applicable to the `vpn_gateway` network type.

`--output json`
:   Optional: Specify whether you want the output displayed in JSON format.

`--help | -h`
:   Optional: Get help on this command.

### Examples
{: #tg-cli-adding-cross-account-connection-transit-gateway-connection-request-examples}

This example illustrates creating a VPC connection named `vpc-connection` that uses `vpcCRN="crn:v1:bluemix:public:is:us-south:a/3aa0a9999a1a46258064d84f7f447920::vpc:r134-f87014d5-87d2-46d1-9999-24683082f6bc"`:

```sh
ibmcloud tg cc $gateway --name vpc-connection --network-id $vpcCRN --network-type vpc
```
{: pre}

To create a classic connection named `classic-conn`.

```sh
ibmcloud tg cc $gateway --name classic-conn --network-account-id 67123579566843320188712647902101 --network-type classic
```
{: pre}

To approve a connection from another account as the network owner, run the following command:

```sh
ibmcloud tg connection-approve|ca GATEWAY_ID CONNECTION_ID [-h, --help]
```
{: pre}

To reject a connection from another account as the network owner, run the following command:

```sh
ibmcloud tg connection-reject|cr GATEWAY_ID CONNECTION_ID [-h, --help]
```
{: pre}

For more information about available commands and options, see [Connections](/docs/transit-gateway?topic=transit-gateway-transit-gateway-cli#connections) in the Transit Gateway command reference.

## Adding a cross-account connection with the API
{: #tg-api-adding-cross-account-connection-transit-gateway}
{: api}

To add a cross-account connection, follow these steps:

1. Request a connection to communicate between other accounts.
1. Perform actions on a requested connection. This must be completed.

For classic cross-account connections, be sure that the `network-account-id` is set to the account you are requesting to communicate with. For VPC cross-account connections, be sure that the `network-id` is set to the account that you are requesting to communicate with.
{: important}

For more information, see [Adds a connection to a Transit Gateway](/apidocs/transit-gateway?code=java#create-transit-gateway-connection) and [Performs actions on a connection for a Transit Gateway](/apidocs/transit-gateway?code=java#create-transit-gateway-connection-actions) in the Transit Gateway API reference.
{: note}

### Request cross-account connection
{: #request-cross-account-connection}

The original account must request a connection to communicate with the other account.

#### Example Request
{: #tg-api-adding-cross-account-connection-transit-gateway-request-example}

This example illustrates the original account requesting a cross-account connection:

```sh
curl -X POST --location --header "Authorization: Bearer {iam_token}" \
  --header "Accept: application/json" \
  --header "Content-Type: application/json" \
  --data '{ "network_type": "vpc" }'
  "
{base_url}/transit_gateways/{transit_gateway_id}/connections?version={version}"
```
{: pre}

```sh
  "name": "Transit_Service_BWTN_SJ_DL",
  "network_id": "crn:v1:bluemix:public:is:us-south:a/123456::vpc:4727d842-f94f-4a2d-824a-9bc9b02c523b",
  "network_type": "vpc",
  "prefix_filters": [
    {
      "action": "permit",
      "ge": 0,
      "le": 32,
      "prefix": "192.168.100.0/24"
    }
  ],
  "prefix_filters_default": "permit",
```
{: pre}

#### Example Response
{: #tg-api-adding-cross-account-connection-transit-gateway-response-example}

This example illustrates the response from a request for a cross-account connection:

```sh
{
  "created_at": "2020-03-31T12:08:05Z",
  "id": "1a15dca5-7e33-45e1-b7c5-bc690e569531",
  "name": "example-connection",
  "network_id": "crn:[...]",
  "network_type": "vpc",
  "status": "pending",
  "updated_at": "2020-03-31T12:08:05Z"
}
```
{: pre}

### Perform actions on a requested connection
{: #tg-api-adding-cross-account-connection-transit-gateway-actions}

After the original account requests a cross-account connection, the other account must perform actions on a requested connection.

#### Example Request
{: #tg-api-adding-cross-account-connection-transit-gateway-actions-request-example}

This example illustrates approving a cross-account connection:

```sh
"
{base_url}/transit_gateways/{transit_gateway_id}/connections/{id}/actions?version={version}"
{
  "action": "approve"
}

```
{: pre}

#### Example Response
{: #tg-api-adding-cross-account-connection-transit-gateway-actions-response-example}

This example illustrates a Status 403 response in which the caller is not authorized to perform the requested action:

```sh
{
  "errors": [
    {
      "code": "missing_field",
      "message": "The `location` field is required.",
      "more_info": "https://transitservice.cloud.ibm.com/",
      "target": {
        "name": "location",
        "type": "field"
      }
    }
  ],
  "trace": "86780a34-e651-4b47-9fb0-184a169cc9af"
}
```
{: pre}

## Adding a connection with Terraform
{: #tg-terraform-adding-cross-connection-transit-gateway}
{: terraform}

Review the following argument references that you can specify for your resource when you create a cross-connection for a transit gateway using Terraform:

|Argument|Details|
|--|--|
|**base_connection_id**  \n Optional  \n Forces new resource \n string | The ID of a network_type 'classic' connection a tunnel is configured over.  \n This field only applies to network type `gre_tunnel` connections.|
|**base_network_type**  \n Optional  \n Forces new resource  \n string | The base network type. Allowed values are `classic`.  \n This field only applies to `unbound_gre_tunnel` type connections.
|**gateway**  \n Required  \n Forces new resource  \n string | Enter the transit gateway identifier.|
|**local_gateway_ip**  \n Optional  \n Forces new resource  \n string | The local gateway IP address. \n This field is required for, and only applicable to, `gre_tunnel` and `unbound_gre_tunnel` type connections. |
|**local_tunnel_ip**  \n Optional  \n Forces new resource  \n string | The local tunnel IP address. \n This field is required for, and only applicable to, `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**name**  \n Optional  \n string | The connection name. If the name is not given, a default name is provided based on the network type, such as `vpc` for network type VPC and `classic` for network type classic.|
|**network_account_id**  \n Optional  \n Forces new resource  \n string|The ID of the network connected account. This is used if the network is in a different account than the gateway.|
|**network_type**  \n Required  \n Forces new resource  \n string | The network type. Allowed values are `classic`, `directlink`, `gre_tunnel`, `unbound_gre_tunnel`, `vpn_gateway`, and `vpc`. |
|**network_id**  \n Optional  \n Forces new resource  \n string | The ID of the network that is being connected to through this connection. \n This parameter is required for network type `vpc` and `directlink`, the CRN of the VPC or direct link gateway to be connected.  \n This field is required to be unspecified for network type `classic`.  \n **Example**:`crn:v1:bluemix:public:is:us-south:a/123456::vpc:4727d842-f94f-4a2d-824a-9bc9b02c523b`|
|**remote_bgp_asn**  \n Optional  \n Forces new resource  \n integer | The remote network BGP ASN (will be generated for the connection if not specified).  \n This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**remote_gateway_ip**  \n Optional  \n Forces new resource  \n string | The remote gateway IP address. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**remote_tunnel_ip**  \n Optional  \n Forces new resource  \n string | The remote tunnel IP address. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections.|
|**zone**  \n Optional  \n Forces new resource  \n string | The location of the GRE tunnel. This field only applies to `gre_tunnel` and `unbound_gre_tunnel` type connections. |
{: caption="Terraform argument references for creating a connection" caption-side="bottom"}

### Example
{: #tg-terraform-adding-cross-connection-transit-gateway-example}

This example illustrates creating a transit gateway cross-connection using Terraform:

```sh
resource "ibm_tg_connection" "test_ibm_tg_connection" {
  gateway      = ibm_tg_gateway.test_tg_gateway.id
  network_type = "vpc"
  name         = "myconnection"
  network_id   = ibm_is_vpc.test_tg_vpc.resource_crn
}
```
{: pre}
