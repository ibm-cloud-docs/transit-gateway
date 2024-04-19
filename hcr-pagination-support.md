---

copyright:
  years: 2024
lastupdated: "2024-04-18"
keywords:

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Preparing for connection lists pagination support
{: #notification-tgw-pagination-support-connections-lists}

**CLI supported version:** v0.8.13 ([Upgrade your CLI version](/docs/cli?topic=cli-ibmcloud_commands_settings#ibmcloud_plugin_update))

**Terraform IBM Cloud Provider supported version:** v1.62 or higher

## What changed?
{: #what-changed}

Starting 20 May 2024, the IBM Cloud Transit Gateway connections list will begin supporting pagination. Currently, the entire list of connections is returned using the REST API and CLI. With pagination, if you have more connections than the requested `limit` (default: API 50/CLI 100, maximum 500) only the number of connections within the size limit are returned, sorted by date with the oldest first.

## Why are we making this change?
{: #why-making-change}

The purpose of this change is to improve performance and reliability.

## What are the effects of this change?
{: #effects-of-this-change}

This change impacts you if you have greater than 50 connections on a transit gateway and use the REST API, CLI, or Terraform to retrieve the list of connections. If you have not updated your tooling to handle the pagination when this change goes into effect, your tools will not return the entire list of connections. For example, if you don't upgrade your CLI client, a maximum of 50 connections are returned.

The SDK automatically handles pagination.
{: note}

## What actions can you take to avoid disruption?
{: #actions-to-take}

Upgrade your CLI and Terraform versions and update your tooling that uses REST API to handle the pagination.

While the default `limit` value allows your existing clients to retrieve the entire list of connections with one request, the default `limit` value is expected to be lowered in a future release. Additionally, we expect the number of transit gateway connections will continue to increase. Therefore, to ensure your clients continue to be aware of all connections, you must upgrade your clients to follow our [pagination guidance](/apidocs/transit-gateway#api-pagination).

## How do you set this optional `limit` value?
{: #set-limit-parameter}

The list of connections uses the default value unless you set a 'limit' value.

* For CLI, use the [`ibmcloud tg connections`](/docs/transit-gateway?topic=transit-gateway-transit-gateway-cli#list-connections) command.
* For API, [retrieve all connections for a transit gateway](/apidocs/transit-gateway#list-connections).
* For Terraform, no action is necessary. When you update the provider version to the recommended version, pagination is handled automatically.

 To test that your clients have been upgraded correctly, specify a `limit` value of `1`.
 {: tip}
