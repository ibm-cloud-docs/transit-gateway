---

copyright:
  years: 2025
lastupdated: "2025-05-29"

keywords:

subcollection: transit-gateway

---

# Monitoring Transit Gateway
{: #monitoring}

[IBM Cloud Monitoring](https://www.ibm.com/products/cloud-monitoring){: external} is a cloud-native and container-intelligent management system that you can include as part of your IBM Cloud architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams, and developers full-stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards.
{: shortdesc}

Service Metrics enable gathering usage and status metrics. Metrics datasets are available on a metrics-enabled instance in the same region. You can visualize and analyze metrics from the respective metrics-enabled instance.

## Platform Metrics overview
{: #platform-metrics-pm}

You can configure only one instance of the {{site.data.keyword.mon_full}} service per region to collect service metrics. Service metrics are enabled by default in all instances, and can't be disabled.

- Provision an instance of the {{site.data.keyword.mon_full_notm}} service. After you provision the Monitoring instance, the *Observability* page opens. To continue working with {{site.data.keyword.cloud_notm}}, go back to the {{site.data.keyword.cloud_notm}} console.
- To configure the Monitoring instance, you must turn on the *service metrics* configuration setting.
- To view metrics for a transit gateway, you must have at least one connection associated with it.
- If a Monitoring instance in a region is already enabled to collect service metrics, metrics from enabled-monitoring services are collected automatically and available for monitoring through this instance. For more information about enabled-monitoring services, see [IBM Cloud Monitoring](https://www.ibm.com/products/cloud-monitoring){: external}.

To monitor service metrics, check that the Monitoring instance is provisioned in the same region where the {{site.data.keyword.cloud_notm}} instance is provisioned.
{: important}

## Metrics available for Transit Gateway
{: #metrics_dictionary-pm}

Each metric is composed of the following metadata types:

* Metric name - The name for the collected metric.
* Metric type - Determines whether the metric value is a counter metric or a gauge metric. Each of these metrics is of the type `gauge`, which represents a single numerical value that can arbitrarily fluctuate over time.
* Value type - A unit of measurement for a specific metric. Examples include bytes or counts. A value type of `none` means that the metric value represents individual occurrences of that metric type.
* Segment - How you want {{site.data.keyword.mon_full_notm}} to divide and display the monitoring metrics.

### ConnectionBpsIngress
{: #ibm_cloud_tranist_gateway_bytes_per_second_ingress}

Bytes per second data for all the ingress data flow on a gateway.

The metric contains the following metadata:

| Metadata | Description |
|----------|-------------|
| Metric name | `ibm_transit_gateway_ingress_bytes_per_seconds` |
| Metric type | `gauge` |
| Value type | `bytes per second`|
| Segment by |`ibm_ctype`, `ibm_scope`,`ibm_location`,`ibm_service_name`, `ibm_resource_name`, `ibm_resource`, `ibm_resource_type`|
{: caption="IBM Cloud Transit Gateway Ingress bytes per second metrics" caption-side="bottom"}

The Segment By labels correspond to the following definitions:

* **ibm_ctype** - Type of cloud instance: `public`
* **ibm_scope** - The account that is associated with a given gateway
* **ibm_location** - Gateway's location
* **ibm_service_name** - `transit`
* **ibm_resource_name** - Gateway's name
* **ibm_resource** - Gateway's resource ID
* **ibm_resource_type** - Type of resource: `gateway`

### Launching {{site.data.keyword.mon_full_notm}} web UI from the Observability page
{: #view_metrics}

Complete the following steps to launch the {{site.data.keyword.mon_full_notm}} web UI from the *Observability* page:

1. [Launch the {{site.data.keyword.mon_full_notm}} web UI](/docs/monitoring?topic=monitoring-launch).
1. Click **DASHBOARDS**.
1. In the **Default Dashboards** section, expand **{{site.data.keyword.IBM_notm}}**.
1. Choose the Transit Overview Dashboard from the list.

   You can also reach your deployment's {{site.data.keyword.mon_full_notm}} dashboard from {{site.data.keyword.mon_full_notm}} in the sidebar, under {{site.data.keyword.IBM_notm}}.

   Next, change the scope or make a copy of the *Default* dashboard to monitor a Transit Gateway instance.

For more options to customize your dashboard, follow the steps in [Creating custom dashboards in the Web UI](/docs/monitoring?topic=monitoring-dashboards#dashboards_create).
