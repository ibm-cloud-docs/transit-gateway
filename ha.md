---

copyright:
  years: 2024, 2025
lastupdated: "2025-06-23"

keywords:

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Understanding high availability for Transit Gateway
{: #ha}

[High availability](#x2284708){: term} (HA) is a core discipline in an IT infrastructure to keep your apps up and running, even after a partial or full site failure. The main purpose of high availability is to eliminate potential points of failures in an IT infrastructure.
{: shortdesc}

{{site.data.keyword.tg_full}} is highly available within any {{site.data.keyword.cloud_notm}} region (for example, Dallas or Washington, DC). However, recovering from disasters that affect an entire region requires planning and preparation.

You are responsible for understanding your configuration, customization, and usage of the service. You are also responsible for being ready to recreate an instance of the service in a new region and restore your data in a new region.
{: important}

{{site.data.keyword.cloud_notm}} supports high availability with no single point of failure. The service achieves high availability automatically and transparently by the multi-zone region ([MZR](/docs/overview?topic=overview-locations#regions)) feature provided by {{site.data.keyword.cloud_notm}}.

When you create a transit gateway instance in a particular region, the system automatically enables multiple zones, which do not share a single point of failure.

Transit gateway GRE connections are point-to-point, have no built-in redundancy, and require the gateway owner to configure high availability (HA) based on their specific needs. When setting up a GRE connection, you must specify the availability zone. For a more robust HA solution, configure multiple GRE connections across different availability zones or use Redundant GRE with at least two tunnels.

See [How IBM Cloud ensures high availability and disaster recovery](/docs/resiliency?topic=resiliency-ha-redundancy#zero-downtime) to learn more about the high availability and disaster recovery standards in {{site.data.keyword.cloud_notm}}. You can also find information about [Service Level Agreements](/docs/overview?topic=overview-slas#slas).

## Responsibilities
{: #ha-responsibilities}

To find out more about responsibility ownership for using Transit Gateway between {{site.data.keyword.IBM_notm}} and the customer, see [Understanding your responsibilities when using Transit Gateway](/docs/transit-gateway?topic=transit-gateway-tg-responsibilities).

## What level of availability do I need?
{: #ha-level}

You can achieve high availability on different levels in your IT infrastructure and within different components of your cluster. The level of availability that is right for you depends on several factors, such as your business requirements, the service level agreements (SLAs) that you have with your customers, and the resources that you want to expend.

## What level of availability does {{site.data.keyword.cloud_notm}} offer?
{: #ha-service}

The level of availability that you set up for your cluster impacts your coverage under the {{site.data.keyword.cloud_notm}} high availability service level agreement terms.

Service level objectives (SLOs) describe the design points that the {{site.data.keyword.cloud_notm}} services are engineered to meet. Transit Gateway is designed to achieve the following availability target.

| Availability target | Target value   |
|---|---|
|  Availability % | 99.999% |
{: caption="SLO for Transit Gateway" caption-side="bottom"}

The SLO is not a warranty and {{site.data.keyword.IBM_notm}} will not issue credits for failure to meet an objective. Refer to the SLAs for commitments and credits that are issued for failure to meet any committed SLAs. For a summary of all SLOs, see [{{site.data.keyword.cloud_notm}} service level objectives](/docs/resiliency?topic=resiliency-slo).

## Locations
{: #ha-locations}

For more information about service availability within regions and data centers, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region).
