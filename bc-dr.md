---

copyright:
  years: 2024
lastupdated: "2024-11-22"

keywords:

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Understanding business continuity and disaster recovery for Transit Gateway
{: #bc-dr}

[Disaster recovery](#x2113280){: term} involves a set of policies, tools, and procedures for returning a system, an application, or an entire data center to full operation after a catastrophic interruption. It includes procedures for copying and storing an installed system's essential data in a secure location, and for recovering that data to restore normalcy of operation.
{: shortdesc}

In the event of a catastrophic failure impacting an entire region, the transit gateway service management plane, which is global, continues to be available. Transit gateway instances are restored when the failing region recovers. However, in some rare cases, you might need to re-create specific instances of your transit gateways and their connections.

Your disaster recovery plan needs to include knowing, preserving, and being prepared to restore all data that is maintained on {{site.data.keyword.cloud_notm}}. This includes data about all deployed transit gateways and their connections.

## Responsibilities
{: #bc-dr-responsibilities}

To find out more about responsibility ownership for using {{site.data.keyword.cloud}} products between {{site.data.keyword.IBM_notm}} and customer see [Understanding your responsibilities when using Transit Gateway](/docs/transit-gateway?topic=transit-gateway-tg-responsibilities).

## Disaster recovery strategy
{: #bc-dr-strategy}

{{site.data.keyword.cloud_notm}} has [business continuity](#x3026801){: term} plans in place to provide for the recovery of services within hours if a disaster occurs. You are responsible for your data backup and associated recovery of your content.

Transit Gateway provides mechanisms to protect your data and restore service functions. Business continuity plans are in place to achieve targeted [recovery point objective](#x3429911){: term} (RPO) and [recovery time objective](#x3167918){: term} (RTO) for the service. The following table outlines the targets for Transit Gateway.

| Disaster recovery objective | Target value |
|---|---|
|  RPO | 24 hrs |
|  RTO | 24 hrs |
{: caption="RPO and RTO for Transit Gateway" caption-side="bottom"}

## Locations
{: #bc-dr-locations}

For more information about service availability within regions and data centers, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region).

## Backing up transit gateways for disaster recovery
{: #disaster-recovery-tgw}

Be prepared to re-create your transit gateways and connections. This section helps you ensure that you have all the data needed for this purpose.

{{site.data.keyword.tg_full_notm}} backups are cross-regionally durable. They are stored across multiple regions, and are restorable to other regions.
{: note}

The following steps use the IBM Cloud CLI, but you can also use the IBM Cloud console or API.
{: tip}

Preserve a list of all of your transit gateways and their connections. To do so, follow these steps:

1. Use the `ibmcloud tg gateways` command to list details about all your transit gateways. Save this output.
1. For each gateway, use the `ibmcloud tg connections GATEWAY_ID` command to list information about its connections. Save this output.

For more information, see the [Transit Gateway CLI reference](/docs/transit-gateway?topic=transit-gateway-transit-gateway-cli).
{: tip}

Saving the information that is returned from these commands helps you recover from a failure quickly. In the event of a failure, use the saved information and run the `ibmcloud tg gateway-create` and `ibmcloud tg connection-create` commands to re-create your transit gateways and connections.
