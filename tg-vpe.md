---

copyright:
  years: 2017, 2021
lastupdated: "2021-03-04"

keywords: vpe

subcollection: transit-gateway

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank_"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:note: .note}
{:important: .important}

# Integrating with Virtual Private Endpoint for VPC
{: #vpe-for-ibm-cloud-transit-gateway}

{{site.data.keyword.cloud}} Virtual Private Endpoint (VPE) for VPC enables you to connect to supported {{site.data.keyword.cloud_notm}} services from your VPC network by using IP addresses of your choosing, allocated from a subnet within your VPC.

## Setting up a VPE gateway for the {{site.data.keyword.tg_short}} service
{: #vpe-setup}

Follow instructions in [Getting started](/docs/vpc?topic=vpc-about-vpe#vpe-getting-started) for VPE for VPC to create and confirgue a VPE gateway for the {{site.data.keyword.tg_short}} service offering.

### Using the CLI
{: #tgw-cli}

After creating an endpoint gateway for {{site.data.keyword.tg_short}}, follow these steps:

1. Update the {{site.data.keyword.cloud_notm}} CLI to the latest version:

   ```sh
   ibmcloud update
   ```
   {: pre}
1. Update the {{site.data.keyword.tg_short}} CLI plug-in:

   ```sh
   ibmcloud plugin update tg-cli
   ```
   {: pre}

### Using the VPE for VPC API
{: #vpe-setup-api}

After creating an endpoint gateway for the {{site.data.keyword.tg_short}} service, use the service endpoint's FQDN  `private.transit.cloud.ibm.com` in the URL to access the service. For example:

```sh
curl https://private.transit.cloud.ibm.com/v1/transit_gateways?version='2020-03-31' -H "Authorization: Bearer $iam_token"
```
{: pre}

### Using the SDK
{: #tgw-sdk}

After creating an endpoint gateway for the {{site.data.keyword.tg_short}} service, you must use the private endpoint's FQDN when setting the service's FQDN during construction of the {{site.data.keyword.tg_short}} service object.

```
private.transit.cloud.ibm.com
```

For examples of setting the service's FQDN for the specific SDK language, see [SDK API examples](/apidocs/transit-gateway?code=go#api-endpoint).  

### Using Terraform
{: #tgw-terrform}

If you plan to access the {{site.data.keyword.tg_short}} service using Terraform, make sure to set the `IBMCLOUD_TG_API_ENDPOINT` environment variable to `private.transit.cloud.ibm.com`. For example:

```sh
export IBMCLOUD_TG_API_ENDPOINT=private.transit.cloud.ibm.com
```
{: pre}

For more information, see [Transit Gateway resources](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-tg-resource) and [Transit Gateway data sources](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-transit-gateway-ds).
