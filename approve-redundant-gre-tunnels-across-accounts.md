---

copyright:
  years: 2020, 2024
lastupdated: "2024-06-12"

keywords: editing, managing, manage, edit, add, connection

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Approving and rejecting cross-account redundant GRE requests
{: #approve-reject-redundant-gre-tunnels}

As the network owner, you can approve or reject a cross-account connection request. However, keep in mind that for redundant GRE requests, approval or rejection is done at the redundant GRE level. You cannot approve or reject individual redundant GRE tunnels. Supply the redundant GRE ID as the connection ID.
{:shortdesc}

## Approving cross-account redundant GRE requests in the UI
{: #tg-ui-approve-reject-redundant-gre-tunnels}
{: ui}

When a [connection request to a network in another account](/docs/transit-gateway?topic=transit-gateway-adding-cross-account-connections&interface=ui) is created, the network owner's account then receives a notification of the request.

To approve a cross-account redundant GRE request from another account in the UI, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Interconnectivity** > **Transit Gateway**.
1. Click the name of the transit gateway in the table.
1. In the Connections section, see **Active required** to view the incoming network connection request.
1. Click **Approve** to approve the request.
1. Click **Approve** to confirm. The status of the network connection indicates Attaching.

When you change back to the original account, the status of the connection changes to **Attached**, indicating that the network request was approved.

## Rejecting cross-account redundant GRE requests in the UI
{: #tg-ui-reject-redundant-gre-tunnels}
{: ui}

To reject a redundant GRE request from another account in the UI, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Navigation Menu icon ![Navigation Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Interconnectivity** > **Transit Gateway**.
1. Click the name of the transit gateway in the table.
1. In the Connections section, see **Active required** to view the incoming network connection request.
1. Click **Reject** to reject the request.
1. Click **Reject** to confirm.

The status of the network connection indicates **Rejected**. The gateway owner's account (or the network owner's account) can now delete the connection.  If the network owner deletes the connection, the gateway owner sees the connection status as **Detached**. If the cross-account connection is not explicitly approved, it expires after 72 hours.

## Approving cross-account redundant GRE requests from the CLI
{: #approve-redundant-gre-tunnels-across-accounts-cli}
{: cli}

As the network owner, to approve a redundant GRE request from another account, run the following command:

```sh
ibmcloud tg connection-approve|ca GATEWAY_ID CONNECTION_ID [-h, --help]
```
{: pre}

Where:

`GATEWAY_ID`
:   ID of the gateway the connection is on.

`CONNECTION_ID`
:   ID of the connection you are approving.

`--help | -h`
:   Optional: Get help on this command.

## Rejecting cross-account redundant GRE requests from the CLI
{: #reject-redundant-gre-tunnels-across-accounts-cli}
{: cli}

As the network owner, to reject a redundant GRE request from another account, run the following command:

```sh
ibmcloud tg connection-reject|cr GATEWAY_ID CONNECTION_ID [-h, --help]
```
{: pre}

Where:

`GATEWAY_ID`
:   ID of the gateway the connection is on.

`CONNECTION_ID`
:   ID of the connection you are rejecting.

`--help | -h`
:   Optional: Get help on this command.

## Approving cross-account redundant GRE requests with the API
{: #tg-api-approve-redundant-gre-connection-transit-gateway}
{: api}

A network owner can approve a redundant GRE request across accounts.
{: shortdesc}

### Example Request
{: #example-request-approve-cross-account-request-api}
{: api}

```sh
curl -X POST https://$TS_ENDPOINT/v1/transit_gateways/$GATEWAY_ID/connections/$CONNECTION_ID/tunnels/$TUNNEL_ID --header "Authorization: Bearer {iam_token}"   --header "Content-Type: application/json"   --data '{ "action": "approve" }'
```
{: pre}

For more information, see [Performs actions on a connection for a Transit Gateway](/apidocs/transit-gateway#create-transit-gateway-connection-actions).
{: note}

## Rejecting cross-account redundant GRE requests with the API
{: #tg-api-reject-redundant-gre-connection-transit-gateway}
{: api}

A network owner can reject a redundant GRE request across accounts.
{: shortdesc}

### Example Request
{: #example-request-approve-cross-account-request-api}
{: api}

```sh
curl -X POST https://$TS_ENDPOINT/v1/transit_gateways/$GATEWAY_ID/connections/$CONNECTION_ID/tunnels/$TUNNEL_ID?version=2020-03-31 --location --header "Authorization: Bearer {iam_token}" --header "Content-Type: application/json" --data '{ "action": "reject" }'
```
{: pre}

For more information, see [Performs actions on a connection for a Transit Gateway](/apidocs/transit-gateway#create-transit-gateway-connection-actions).
{: note}

## Approving cross-account redundant GRE requests using Terraform
{: #tg-terraform-approve-redundant-gre-connection-transit-gateway}
{: terraform}

To use Terraform, download the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in. For more information, see [Getting started with Terraform](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started).
{: requirement}

The following example illustrates approving a redundant GRE across accounts:

```terraform
resource "ibm_tg_connection_action" "test_tg_cross_connection_approval" {
    provider = ibm.account2
    gateway = ibm_tg_gateway.new_tg_gw.id
    connection_id = ibm_tg_connection.test_ibm_tg_connection.connection_id
    action = "approve"
}
```
{: pre}

For more information, see the [Terraform registry](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/tg_connection_actions){: external}.

Tunnel-level approval is not allowed.
{: note}

## Rejecting cross-account redundant GRE requests using Terraform
{: #tg-terraform-reject-redundant-gre-connection-transit-gateway}
{: terraform}

The following example illustrates rejecting a redundant GRE across accounts:

```terraform
resource "ibm_tg_connection_action" "test_tg_cross_connection_approval" {
    provider = ibm.account2
    gateway = ibm_tg_gateway.new_tg_gw.id
    connection_id = ibm_tg_connection.test_ibm_tg_connection.connection_id
    action = "reject"
}
```
{: pre}

For more information, see the [Terraform registry](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/tg_connection_actions){: external}.

Tunnel-level rejection is not allowed.
{: note}

## Related link
{: #related-links-approve-reject-connection-requests}

* [Adding a cross-account connection](/docs/transit-gateway?topic=transit-gateway-adding-cross-account-connections&interface=ui)
