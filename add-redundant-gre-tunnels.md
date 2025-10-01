---

copyright:
  years: 2020, 2025
lastupdated: "2025-10-01"

keywords:

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Adding and removing redundant GRE tunnels
{: #add-remove-redundant-gre-tunnels}

You can add or remove tunnels attached to GRE redundant connections. Keep in mind that a minimum of two GRE tunnels are required.

## Before you begin
{: #add-remove-redundant-gre-planning}

Before you add a tunnel to a redundant GRE, make sure to review [General](/docs/transit-gateway?topic=transit-gateway-helpful-tips#gre-general-considerations) and [Redundant](/docs/transit-gateway?topic=transit-gateway-helpful-tips#redundant-gre-connection-considerations) GRE considerations.

## Adding a tunnel to a redundant GRE in the UI
{: #tg-ui-adding-redundant-gre-tunnels}
{: ui}

You can add tunnels when [creating a redundant GRE](/docs/transit-gateway?topic=transit-gateway-redundant-gre-connection&interface=ui), or after provisioning an existing transit gateway with a redundant GRE. To add a tunnel to an existing redundant GRE, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**.
1. Click the name of the transit gateway where you want to add a tunnel.
1. In the Connections tabbed view, click the Actions menu ![Actions icon](../icons/action-menu-icon.svg "Actions") at the end of the table row of the connection where you want to add a tunnel.

   If you expand the row of the connection, tunnel details and their states are listed.
   {: note}

1. Click **Add tunnel**. You can add more tunnels, but you can't exceed two tunnels per zone.
1. In the Add tunnel window, choose an availability zone in which to create the tunnel. Then, complete the following fields.

   When you select a zone for the tunnel, only valid zones for a GRE connection are shown as options.
   {: note}

   1. Optionally, enter the remote BGP ASN, which is a valid 2 or 4-byte value of your choosing. If you leave this field blank, a unique ASN is assigned.
   1. Enter the local gateway IP that the transit gateway uses to host the underlay network for the GRE tunnel. This user-selected IP address is configured on the transit gateway GRE tunnel after it is created.
   1. Enter the remote gateway IP for the endpoint of the GRE tunnel.
   1. Enter a `/30` local tunnel IP for both ends of the tunnel, for example `192.168.103.1`.
   1. Enter a `/30` remote tunnel IP for both ends of the tunnel, for example `192.168.103.2`.
   1. Enter a connection name for your GRE tunnel.

1. Click **Add** to create the tunnel.

## Removing a tunnel from a redundant GRE in the UI
{: #tg-ui-removing-redundant-gre-tunnels}
{: ui}

To remove a tunnel from a redundant GRE, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**.
1. Click the name of the transit gateway where you want to remove a tunnel.
1. In the Connections tabbed view, click the Actions menu ![Actions icon](../icons/action-menu-icon.svg "Actions") at the end of the table row of the connection where you want to remove a tunnel.

   If you expand the row of the connection, tunnel details and their states are listed.
   {: note}

1. Click **Remove tunnel**.
1. In the Delete GRE tunnel window, select the name of the GRE tunnel that you want to remove, then click **Delete**. You can't undo this action.

A connection can't have less than two tunnels attached to a redundant GRE.
{: important}

## Adding a tunnel to a redundant GRE from the CLI
{: #add-tunnel-redundant-gre-cli}
{: cli}

You can add a tunnel to a redundant GRE by using the CLI options or a JSON file.  The command syntax to add a tunnel using CLI options is as follows:

```sh
ibmcloud tg redundant-gre-tunnel-add|targre GATEWAY_ID REDUNDANT_GRE_ID --name NAME --zone ZONE --local-gateway-ip LOCAL_GATEWAY_IP --local-tunnel-ip  LOCAL_TUNNEL_IP --remote-gateway-ip REMOTE_GATEWAY_IP --remote-tunnel-ip REMOTE_TUNNEL_IP [--remote-bgp-asn REMOTE_BGP_ASN] [--output json]
```
{: pre}

Where:

`GATEWAY_ID`
:   ID of the gateway where the new connection is bound.

`REDUNDANT_GRE_ID`
:   ID of the redundant GRE.

`--name`
:   Name of the new tunnel.

`--zone`
:   Availability zone for the GRE tunnel. Example: `us-south-1`

`--local-gateway-ip`
:   Local gateway IP address[^ip2] for the GRE tunnel connection.

`--local-tunnel-ip`
:   Local tunnel IP address for the GRE tunnel connection.

`--remote-gateway-ip`
:   Remote gateway IP address for the GRE tunnel connection.

`--remote-tunnel-ip`
:   Remote tunnel IP address for the GRE tunnel connection.

`--remote-bgp-asn`
:   Optional: If the remote BGP ASN is not specified, one is generated.

`--output json`
:   Optional: Specify whether you want the output that is displayed in JSON format.

`--help | -h`
:   Optional: Get help on this command.

To add a tunnel that uses a JSON file as input, enter the following command:

```sh
ibmcloud tg redundant-gre-tunnel-add|targre JSON_FILE_PATH [--output json]
```
{: pre}

JSON file example:

```json
{
  "gateway_id": "47f11b01-471c-47d0-9e84-550c88c94055",
  "redundant_gre_id": "83792525-471c-47d0-9e84-jdy830jd",
  "name": "unbound_gre_tunnel",
  "local_gateway_ip": "192.168.100.1",
  "local_tunnel_ip": "192.168.129.2",
  "remote_bgp_asn": 65010,
  "remote_gateway_ip": "10.242.63.12",
  "remote_tunnel_ip": "192.168.129.1",
  "zone": {
      "name": "us-south-1"
        }
}
```
{: pre}

## Removing a tunnel from a redundant GRE from the CLI
{: #remove-tunnel-redundant-gre}
{: cli}

To remove a tunnel from a redundant GRE, enter the following command:

```sh
ibmcloud tg redundant-gre-tunnel-remove|trrgre GATEWAY_ID REDUNDANT_GRE_ID TUNNEL_ID [--force | -f ] [--help | -h]
```
{: pre}

Where:

`GATEWAY_ID`
:   ID of the gateway where the connection is bound.

`REDUNDANT_GRE_ID`
:   ID of the redundant GRE.

`TUNNEL_ID`
:   ID of the tunnel to be deleted.

`--force | -f`
:   Optional: Force the delete without confirmation.

`--help | -h`
:   Optional: Get help on this command.


## Adding a tunnel to a redundant GRE with the API
{: #add-tunnel-redundant-gre-api}
{: api}

You can add a tunnel to an existing redundant GRE with the API.

### Example Request
{: #add-tunnel-redundant-gre-api-request-example}

```sh
curl -H "Content-Type: application/json" -X POST https://$TS_ENDPOINT/v1/transit_gateways/$GATEWAY_ID/connections/$CONNECTION_ID/tunnels?version=2020-03-31   -H "authorization: Bearer $IAM_TOKEN"   -d '{
  "local_gateway_ip": "192.168.100.1",
  "local_tunnel_ip": "192.168.129.2",
  "name": "gre1",
  "remote_bgp_asn": 65010,
  "remote_gateway_ip": "10.242.63.12",
  "remote_tunnel_ip": "192.168.129.1",
  "zone": {
    "name": "us-south-1"
  }
}'
```
{: pre}

### Example Response
{: #add-tunnel-redundant-gre-api-response-example}

```json
{
  "name": "gre1",
  "id": "47f11b01-471c-47d0-9e84-550c88c94057",
  "mtu": 9000,
  "status": "up",
  "updated_at": "2024-06-10T14:52:54.918Z",
  "created_at": "2024-06-10T14:52:54.918Z",
  "local_gateway_ip": "192.168.200.1",
  "local_tunnel_ip": "192.168.239.2",
  "remote_gateway_ip": "10.242.63.12",
  "remote_tunnel_ip": "192.168.129.1",
  "local_bgp_asn": 64490,
  "remote_bgp_asn": 65010,
  "zone": {
    "name": "us-south-1"
  }
}
```
{: screen}

For more information, see [Adding a connection to a Transit Gateway](/apidocs/transit-gateway#create-transit-gateway-gre-tunnel) in the Transit Gateway API reference.
{: note}

## Removing a tunnel from a redundant GRE with the API
{: #remove-tunnel-redundant-gre-api}
{: api}

You can add a tunnel to an existing redundant GRE with the API as long as it has more than two tunnels:

```sh
curl -X DELETE https://$TS_ENDPOINT/v1/transit_gateways/$GATEWAY_ID/connections/$CONNECTION_ID/tunnels/$TUNNEL_ID?version=2020-03-31   -H "authorization: Bearer $IAM_TOKEN"
```
{: pre}

An HTTP `204` code is returned on successful deletion with no response body. For API parameters and examples, see [Deletes specified Transit Gateway redundant GRE tunnel](/apidocs/transit-gateway#delete-transit-gateway-connection-tunnels) in the Transit Gateway API reference.

## Adding a tunnel to a redundant GRE using Terraform
{: #add-tunnel-redundant-gre-terraform}
{: terraform}

To use Terraform, download the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in. For more information, see [Getting started with Terraform](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started).
{: requirement}

The following example illustrates adding a redundant GRE tunnel using Terraform:

```sh
resource "ibm_tg_connection_rgre_tunnel" "test_ibm_tg_connection_tunnel" {
  gateway = ibm_tg_gateway.test_tg_gateway.id
  connection_id = ibm_tg_connection.test_ibm_tg_connection.connection_id
  local_gateway_ip = "192.139.200.1"
  local_tunnel_ip = "192.178.239.2"
  name =  "tunnel_name"
  remote_gateway_ip = "10.186.203.4"
  remote_tunnel_ip = "192.178.239.1"
  zone =  "us-south-3"
}
```
{: pre}

For more information, see the [Terraform registry](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/tg_connection){: external}.

## Removing a tunnel from a redundant GRE using Terraform
{: #remove-tunnel-redundant-gre-terraform}
{: terraform}

The following example illustrates removing a tunnel to a redundant GRE using Terraform:

```sh
terraform destroy -target=ibm_tg_connection_rgre_tunnel.test_ibm_tg_connection_tunnel
```
{: pre}

For more information, see the [Terraform registry](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/tg_connection){: external}.
