---

copyright:
  years: 2020, 2021
lastupdated: "2021-04-16"

keywords: connecting, region, order, ha, recovery, disaster

subcollection: transit-gateway

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}
{:external: target="_blank" .external}
{:term: .term}

# High availability and disaster recovery
{: #ha-dr}

{{site.data.keyword.tg_full}} is highly available within any {{site.data.keyword.cloud_notm}} location (for example, Dallas or Washington, DC). However, recovering from disasters that affect an entire location requires planning and preparation.
{: shortdesc}

You are responsible for understanding your configuration, customization, and usage of the service. You are also responsible for being ready to re-create an instance of the service in a new location and restore your data in a new location.

## High availability
{: #high-availability}

{{site.data.keyword.cloud_notm}} supports high availability with no single point of failure. The service achieves high availability automatically and transparently by means of the multi-zone region ([MZR](/docs/overview?topic=overview-locations#mzr-table)) feature provided by {{site.data.keyword.cloud_notm}}.

When you create a transit gateway instance in a particular region, the system automatically enables multiple zones which do not share a single point of failure.

## Disaster recovery
{: #disaster-recovery}

In the event of a catastrophic failure impacting an entire region, the transit gateway service management plane, which is global, continues to be available. Transit gateway instances are restored when the failing region recovers. However, in some rare cases, you may need to recreate specific instances of your transit gateways, as well as their connections.

Your disaster recovery plan should include knowing, preserving, and being prepared to restore all data that is maintained on {{site.data.keyword.cloud_notm}}. This includes data about all deployed transit gateways and their connections.

### Backing up transit gateways for disaster recovery
{: #disaster-recovery-tgw}

You must be prepared to recreate your transit gateways and connections. This section helps you ensure you have all the data needed for this purpose.

{{site.data.keyword.tg_full_notm}} backups are cross-regionally durable. They are stored across multiple regions, and are restorable to other regions.
{: note}

The following steps use the IBM Cloud CLI, but you can also use the IBM Cloud console or API.
{: tip}

Preserve a list of all of your transit gateways and their connections. To do so, perform the following procedure:

1. Use the `ibmcloud tg gateways` command to list details about all your transit gateways. Save this output.
2. For each gateway, use the `ibmcloud tg connections GATEWAY_ID` command to list information about its connections. Save this output.

For more information, see the [Transit Gateway CLI reference](/docs/transit-gateway?topic=tg-cli-plugin-transit-gateway-cli).
{: tip}

Saving the information returned from these commands will help you recover from a failure quickly. In the event of a failure, use the saved information and run the `ibmcloud tg gateway-create` and `ibmcloud tg connection-create` commands to recreate your transit gateways and connections.
