---

copyright:
  years: 2020, 2025
lastupdated: "2025-07-28"

keywords: activity tracker, event, security

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Activity tracking events for {{site.data.keyword.tg_full_notm}}
{: #at_events}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.tg_full_notm}}, generate activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service, to route auditing events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

Activity tracker events are captured for all locations, even if recorded in `eu-de`. Because Transit Gateway is a global control plan, if you perform an action to a resource in `us-south`, it's handled by that control plane and logged in the `us-south` location (by default).
{: remember}

## Locations where activity tracking events are generated
{: #at-locations}

By default, Transit Gateway activity tracking events are stored in the Frankfurt (eu-de) location. If you prefer not to store these events in this region, you can set up your AT log routing rules to route to an AT instance in a different location.

## Viewing activity tracking events for {{site.data.keyword.vpc_short}}
{: #at-viewing}

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch}

For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

## List of management events
{: #at_actions}

The following table lists actions that generate management events.

| Action             | Description      |
|--------------------|------------------|
| `transit.gateway.create` | Create a transit gateway     |
| `transit.gateway.delete` | Delete a transit gateway     |
| `transit.gateway.update` | Update a transit gateway     |
| `transit.connection.create` | Create a transit gateway connection   |
| `transit.connection.delete` | Delete a transit gateway connection   |
| `transit.connection-request.delete` | Delete a transit gateway cross account connection   |
| `transit.connection.update` | Update a transit gateway connection   |
| `transit.connection-request.create` | Create a request for a cross account transit gateway connection   |
| `transit.connection-request.approve` | Approve request for a cross account transit gateway connection   |
| `transit.connection-request.reject` | Reject request for a cross account transit gateway connection   |
{: caption="Actions that generate management events" caption-side="bottom"}

## List of data events
{: #at_actions_data}

The following table lists actions that generate data events.

| Action                           | Description                        |
|----------------------------------|------------------------------------|
| `transit.gateway.read` | Retrieve a transit gateway     |
| `transit.gateway.list` | List transit gateways     |
| `transit.connection.list` | List transit gateway connections   |
| `transit.location.read` | Retrieve a transit gateway location   |
| `transit.location.list` | List transit gateway locations   |
{: caption="Actions that generate data events" caption-side="bottom"}

## Analyzing {{site.data.keyword.tg_full_notm}} activity tracking events
{: #at_events_iam_analyze}

Refer to the following information when analyzing events:

* Filter for the `transit` action to see all transit gateway events in your account. Filter for `transit.connection` to see events related to your transit gateway connections.

* Each event's target field identifies which transit gateway is associated with the event.

   When the gateway exists in a different account or there is no associated gateway, the target is set as `crn:v1:bluemix:public:transit:global:a/<your account ID>:::`. Events that don't correspond to a gateway will not have resource group information.

* Events that are associated with a specific connection will include the connection's id in `target.connectionId`.

* Events that report update actions don't include information about the delta of the change.

* The event's initiator field contains information about who initiated each request. In authorized cross account scenarios, `IBM` will be identified as the initiator.
