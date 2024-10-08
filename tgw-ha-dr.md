---

copyright:
  years: 2020, 2024
lastupdated: "2024-08-29"

keywords: connecting, region, order, ha, recovery, disaster

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# High availability and disaster recovery
{: #ha-dr}

{{site.data.keyword.tg_full}} is highly available within any {{site.data.keyword.cloud_notm}} region (for example, Dallas or Washington, DC). However, recovering from disasters that affect an entire region requires planning and preparation.
{: shortdesc}

You are responsible for understanding your configuration, customization, and usage of the service. You are also responsible for being ready to recreate an instance of the service in a new region and restore your data in a new region.

## High availability
{: #high-availability}

{{site.data.keyword.cloud_notm}} supports high availability with no single point of failure. The service achieves high availability automatically and transparently by the multi-zone region ([MZR](/docs/overview?topic=overview-locations#regions)) feature provided by {{site.data.keyword.cloud_notm}}.

When you create a transit gateway instance in a particular region, the system automatically enables multiple zones, which do not share a single point of failure.

Transit gateway GRE connections require the gateway owner to configure HA to meet their specific needs. When you configure a GRE connection on a transit gateway, you must specify the availability zone. For a more robust solution, configure multiple connections that use different availability zones.

Transit gateway GRE connections require the gateway owner to specifically configure HA for their needs. A GRE connection is a point-to-point connection, has no built-in redundancy, and is a single point of failure. When you configure a GRE connection on a transit gateway, you must specify the availability zone. For a robust HA solution, configure multiple GRE connections that use different availability zones.
{: note}

## Disaster recovery
{: #disaster-recovery}

In the event of a catastrophic failure impacting an entire region, the transit gateway service management plane, which is global, continues to be available. Transit gateway instances are restored when the failing region recovers. However, in some rare cases, you might need to re-create specific instances of your transit gateways and their connections.

Your disaster recovery plan needs to include knowing, preserving, and being prepared to restore all data that is maintained on {{site.data.keyword.cloud_notm}}. This includes data about all deployed transit gateways and their connections.

### Backing up transit gateways for disaster recovery
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
