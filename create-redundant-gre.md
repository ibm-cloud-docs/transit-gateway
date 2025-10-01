---

copyright:
  years: 2020, 2025
lastupdated: "2025-10-01"

keywords: editing, managing, manage, edit, add, connection

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Creating a redundant GRE
{: #redundant-gre-connection}

This connection type builds in redundancy and eliminates the need to schedule an outage when a transit gateway is taken offline for maintenance. This connection type allows Generic Routing Encapsulation (GRE) tunnels to be placed on different devices in the same zone and not flag overlapping routes that are in the redundant GRE's tunnels.
{: shortdesc}

Unlike an unbound GRE tunnel that can be connected to only classic networks, a redundant GRE tunnel can connect a transit gateway to either VPC or classic infrastructure endpoints.

## Before you begin
{: #redundant-gre-begin}

Before you create a redundant GRE, read the following planning considerations:

* Review [General](/docs/transit-gateway?topic=transit-gateway-helpful-tips#gre-general-considerations) and [Redundant](/docs/transit-gateway?topic=transit-gateway-helpful-tips#redundant-gre-connection-considerations) GRE considerations.
* You must enter the following four IP addresses when you add a tunnel to a redundant GRE.

   * **Remote gateway IP** - IP address of your GRE tunnel endpoint. This IP address must be a private IP from either a VPC or Classic environment, such as the private IP of a hardware appliance, a virtual server instance, or even a VM.
   * **Local gateway IP** - IP address that your tunnel endpoint connects to. This IP is the transit gateway's IP for establishing the tunnel so that when you enter the **Remote tunnel IP** on your tunnel endpoint, you use this IP address.
   * **Local tunnel IP** - GRE tunnel address on the transit gateway side.
   * **Remote tunnel IP** - GRE tunnel address on the tunnel endpoint.

## Creating a redundant GRE in the UI
{: #tg-ui-adding-redundant-gre-connection-transit-gateway}
{: ui}

You can create a redundant GRE on an existing transit gateway, or when you create a transit gateway.

To create a redundant GRE, follow these steps:

1. Select one of the following choices:

   * To create a redundant GRE while creating a transit gateway:
      1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
      1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**.
      1. Click **Create**.
      1. Enter the transit gateway name, resource group, and location.

   * To create a redundant GRE on an existing transit gateway:
      1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
      1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**.
      1. Click the name of the transit gateway where you want to add a connection.
      1. Click **Add connection** in the Connections tab.

1. Select **Redundant GRE** as your network connection type.
1. Enter the connection name.
1. Select the base network type (**Classic infrastructure** or **VPC**) and whether this is a connection to a network in another account. If you select **VPC** as the base network, you can select the region and VPC that you want to target.

   Prefixes of the base network are not advertised to the transit gateway.
   {: note}

1. If this connection is to a network in another account, enter the account ID and the cloud resource name (CRN) of the VPC.

   For cross accounts, all tunnels in a redundant GRE target the same account. Cross-account approval is for the redundant GRE and all tunnels under the GRE will be accepted or rejected.
   {: important}

   To find the CRN, click **Navigation Menu** ![Navigation Menu icon](../../icons/icon_hamburger.svg) > **Resource List** from the {{site.data.keyword.cloud_notm}} console. Expand the Networking section, then click the table row of the Virtual Private Cloud whose CRN you want to find. The VPC CRN is shown in the details on the Overview tab.
   {: tip}

1. Add a minimum of of two GRE tunnels for this connection.  

   You can click **Add tunnel** to add more tunnels, but you can't exceed two tunnels per zone.
   {: important}

   1. Select an availability zone in which to create the tunnels. When you select a zone for the tunnel, only valid zones for a redundant GRE are shown as options.
   1. Optionally, enter the remote BGP ASN, which is a valid 2 or 4-byte value of your choosing. If you leave this field blank, a unique ASN is assigned.
   1. Enter the remote gateway IP for the endpoint of the GRE tunnel.
   1. Enter the local gateway IP that the transit gateway uses to host the underlay network for the GRE tunnel. This user-selected IP address is configured on the transit gateway GRE tunnel after it is created.
   1. Enter a `/30` local tunnel IP for both ends of the tunnel, for example `192.168.103.1`.
   1. Enter a `/30` remote tunnel IP for both ends of the tunnel, for example `192.168.103.2`.
   1. Enter a connection name for your GRE tunnel.

1. Depending on where you started this procedure, click either **Add** or **Create** to create the redundant GRE.

After you create the redundant GRE, you can expand the redundant GRE section to show its details, including the date created, name, zone, and status.

### Next steps
{: #tgw-next-step-redundant-gre}

To configure the other end of the BGP tunnel, expand the newly created redundant GRE tunnels in the Connections page to see GRE details. It shows the local BGP ASNs. If you created optional remote BGP ASNs, these also show in the Connections page. Give this ASN information to the person creating the other end of the BGP tunnel so that the BGP session can be fully configured.

## Creating a redundant GRE from the CLI
{: #create-redundant-gre-tunnel-connection-cli}
{: cli}

To create a redundant GRE from the CLI, you must use a JSON file as input.

```sh
ibmcloud tg connection-rgre-create|crgrec --file JSON_FILE_PATH [--output json]
```
{: pre}

JSON file:

```json
{
    "gateway_id": "47f11b01-471c-47d0-9e84-550c88c94055",
    "name": "redundant_gre1",
    "network_type": "redundant_gre",
    "base_network_type": "classic",
    "network_account_id": "28e4d90ac7504be694471ee66e70d0d5",
    "network_id": "crn:v1:bluemix:public:is:us-south:a/123456::vpc:4727d842-f94f-4a2d-824a-9bc9b02c523b",
    "tunnels": [
       {
          "local_gateway_ip": "192.168.100.1",
          "local_tunnel_ip": "192.168.129.2",
          "name": "gre1",
          "remote_bgp_asn": "65010",
          "remote_gateway_ip": "10.242.63.12",
          "remote_tunnel_ip": "192.168.129.1",
          "zone": {
             "name": "us-south-1"
          }
       }, {
          "local_gateway_ip": "192.168.101.1",
          "local_tunnel_ip": "192.168.128.2",
          "name": "gre2",
          "remote_bgp_asn": "65010",
          "remote_gateway_ip": "10.242.63.12",
          "remote_tunnel_ip": "192.168.128.1",
          "zone": {
             "name": "us-south-1"
          }
       }
    ]
}
```
{: pre}

### Command options
{: #redundant-gre-command-options-cli}
{: cli}

`gateway_id`
:   ID of the gateway that the new redundant GRE is on.

`name`
:   Name of the new redundant GRE.

`network_type`
:   Network type of the connection. Value is `redundant_gre`.

`base_network_type`
:   The type of network to use. Options are `classic` and `vpc`.

`network_account_id`
:   ID of the IBM Cloud account to use for a cross-account classic network. Only used with `classic` type, when the account of the connection is different than the gateway's account. This option is not valid for the `vpc` base network type.

`network_id`
:   The CRN of the VPC network to use. This option is not valid for the `classic` base network type. To find the CRN of a VPC, enter the following command:

   ```sh
   ibmcloud is vpc VPC_ID --json
   ```
   {: pre}

`tunnels`
:   Collection of all tunnels for this redundant GRE.

`local_gateway_ip`
:   Local gateway IP address for the GRE tunnel connection. This IP address must not be an IP address within the multicast range of `224.0.0.0` to `239.255.255.255` and can't be in conflict with any existing networks that are connected to the transit gateway.

`local_tunnel_ip`
:   Local tunnel IP address for the GRE tunnel connection.

`name`
:   Name of the GRE tunnel.

`remote_bgp_asn`
:   Optional: If the remote BGP ASN is not specified, one is generated.

`remote_gateway_ip`
:   Remote gateway IP address for the GRE tunnel connection.

`remote_tunnel_ip`
:   Remote tunnel IP address for the GRE tunnel connection.

`zone`
:   Availability zone for the GRE tunnel. Example: `us-south-1`

## Creating a redundant GRE with the API
{: #tg-api-adding-redundant-gre-connection-transit-gateway}
{: api}

You can create a redundant Generic Routing Encapsulation (GRE) tunnel connection with the API.

### Example Request
{: #add-redundant-gre-connection-curl-api-request-example}

This example shows how to create a redundant GRE:

```sh
curl -H "Content-Type: application/json" -X POST https://$TS_ENDPOINT/v1/transit_gateways/$GATEWAY_ID/connections?version=2020-03-31   -H "authorization: Bearer $IAM_TOKEN"   -d '{
	"name": "mtp_RGRE",
	"network_type": "redundant_gre",
	"base_network_type": "vpc",
	"network_id": "crn:v1:staging:public:is:us-south:a/aacb87da80cc4a47b9a196fc1713d42d::vpc:r134-285026fa-1d90-4d67-b512-028f4fd8a112",
	"tunnels": [
		{
			"name": "mtp_vpc_tun1",
			"local_gateway_ip": "192.168.200.1",
			"local_tunnel_ip": "192.168.239.2",
			"remote_gateway_ip": "10.240.0.4",
			"remote_tunnel_ip": "192.168.239.1",
			"zone": {
				"name": "us-south-3"
			}
		},
		{
			"name": "mtp_vpc_tun2",
			"local_gateway_ip": "192.168.201.1",
			"local_tunnel_ip": "192.168.238.2",
			"remote_gateway_ip": "10.240.0.4",
			"remote_tunnel_ip": "192.168.238.1",
			"zone": {
				"name": "us-south-3"
			}
		}
	]
}'
```
{: pre}

### Example Response
{: #add-redundant-gre-connection-response-example}

```json
{
   "name": "mtp_RGRE",
   "network_type": "redundant_gre",
   "base_network_type": "vpc",
   "id": "47f11b01-471c-47d0-9e84-550c88c94056",
   "created_at": "22024-06-10T14:52:54.918Z",
   "updated_at": "2024-06-10T14:52:54.918Z",
   "status": "up",
   "tunnels": [
      {
         "name": "mtp_vpc_tun1",
         "id": "47f11b01-471c-47d0-9e84-550c88c94057",
         "mtu": 9000,
         "status": "up",
         "updated_at": "2024-06-10T14:52:54.918Z",
         "created_at": "2024-06-10T14:52:54.918Z",
         "local_gateway_ip": "192.168.200.1",
         "local_tunnel_ip": "192.168.239.2",
         "remote_gateway_ip": "10.240.0.4",
         "remote_tunnel_ip": "192.168.239.1",
         "local_bgp_asn": 64490,
         "remote_bgp_asn": 65010,
         "zone": {
            "name": "us-south-3"
         }
      },
      {
         "name": "mtp_vpc_tun2",
         "id": "47f11b01-471c-47d0-9e84-550c88c94058",
         "mtu": 9000,
         "status": "up",
         "updated_at": "2024-06-10T14:52:54.918Z",
         "created_at": "2024-06-10T14:52:54.918Z",
         "local_gateway_ip": "192.168.201.1",
         "local_tunnel_ip": "192.168.238.2",
         "remote_gateway_ip": "10.240.0.4",
         "remote_tunnel_ip": "192.168.238.1",
         "local_bgp_asn": 64490,
         "remote_bgp_asn": 65011,
         "zone": {
            "name": "us-south-3"
         }
      }
   ]
}
```
{: screen}

For more information, see [Adding a connection to a Transit Gateway](/apidocs/transit-gateway#create-transit-gateway-connection) in the Transit Gateway API reference.
{: note}

## Creating a redundant GRE using Terraform
{: #tg-terraform-adding-redundant-gre-connection-transit-gateway}
{: terraform}

To use Terraform, download the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in. For more information, see [Getting started with Terraform](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started).
{: requirement}

The following example illustrates creating a redundant GRE and adding its tunnels using Terraform:

```sh
resource "ibm_tg_connection" "test_ibm_tg_rgre_connection" {
  gateway      = ibm_tg_gateway.test_tg_gateway.id
  name = redundant_ugre_vpc
  network_type = redundant_gre
  base_network_type = vpc
  network_id = ibm_is_vpc.test_tg_vpc.resource_crn
  tunnels {
           local_gateway_ip = "192.129.200.1"
           local_tunnel_ip = "192.158.239.2"
           name =  "tunne1_testtgw1461"
           remote_gateway_ip = "10.186.203.4"
           remote_tunnel_ip = "192.158.239.1"
           zone =  "us-south-1"
        }
 tunnels {
             local_gateway_ip = "192.129.220.1"
             local_tunnel_ip = "192.158.249.2"
             name =  "tunne2_testtgw1462"
             remote_gateway_ip = "10.186.203.4"
             remote_tunnel_ip = "192.158.249.1"
             zone =  "us-south-1"
         }
}
```
{: pre}

For more information, see the [Terraform registry](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/tg_connection){: external}.

## Related links
{: #gre-related-links}

* [Adding and removing redundant GRE tunnels](/docs/transit-gateway?topic=transit-gateway-add-remove-redundant-gre-tunnels&interface=cli)
* [Approving and rejecting redundant GRE tunnels across accounts](/docs/transit-gateway?topic=transit-gateway-approve-reject-redundant-gre-tunnels&interface=cli)
