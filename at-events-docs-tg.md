---

copyright:
  years: 2020, 2021
lastupdated: "2021-08-23"

keywords: activity tracker, event, security

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Activity Tracker events for {{site.data.keyword.tg_full_notm}}
{: #at_events}

As a security officer, auditor, or manager, you can use the Activity Tracker service to track how users and applications interact with the {{site.data.keyword.tg_full}} service in {{site.data.keyword.cloud_notm}}.
{: shortdesc}

{{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard. For more information, see the [getting started tutorial for {{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started).

On 23 August 2021, some Activity Tracker events for IBM Cloud Transit Gateway changed. For details and required actions, see the [IBM Cloud announcement](https://www.ibm.com/cloud/blog/announcements/the-ibm-cloud-transit-gateway-service-is-changing-ibm-cloud-activity-tracker-events){: external}.
{: important}

## List of events: Gateway resources
{: #at_events_list}

### List of management events
{: #at_management_events}

| Action             | Description      |
|:-------------------|:-----------------|
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
{: caption="Table 1. Actions that generate management events for gateway resources" caption-side="bottom"}

### List of data events
{: #at_data_events}

| Action             | Description      |
|:-------------------|:-----------------|
| `transit.gateway.read` | Retrieve a transit gateway     |
| `transit.gateway.list` | List transit gateways     |
| `transit.connection.list` | List transit gateway connections   |
| `transit.location.read` | Retrieve a transit gateway location   |
| `transit.location.list` | List transit gateway locations   |
{: caption="Table 2. Actions that generate data events for gateway resources" caption-side="bottom"}

## Viewing events
{: #at_ui}

Events are available in the **Frankfurt** location (`eu-de` region) only. {{site.data.keyword.at_full_notm}} can have only one instance per location.

You can view events by accessing the web UI of the {{site.data.keyword.at_full_notm}} service in the `eu-de` region. For more information, see [Launching the UI through the IBM Cloud UI](/docs/activity-tracker?topic=activity-tracker-launch#launch_cloud_ui).

## Analyzing events
{: #at_analyze_events}

Refer to the following information when analyzing events:

* Filter for the `transit` action to see all transit gateway events in your account. Filter for `transit.connection` to see events related to your transit gateway connections.

* Each event's target field identifies which transit gateway is associated with the event.

   When the gateway exists in a different account or there is no associated gateway, the target is set as `crn:v1:bluemix:public:transit:global:a/<your account ID>:::`. Events that don't correspond to a gateway will not have resource group information.

* Events that are associated with a specific connection will include the connection's id in `target.connectionId`.

* Events that report update actions do not include information about the delta of the change.

* The event's initiator field contains information about who initiated each request. In authorized cross account scenarios, `IBM` will be identified as the initiator.
