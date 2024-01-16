---

copyright:
  years: 2024
lastupdated: "2024-01-08"
keywords: api

subcollection: transit-gateway


---

{{site.data.keyword.attribute-definition-list}}

<!--Name your file `service-endpoints.md` with the title Using service endpoints to privately connect to _servicename_. When nav titles are available you can use Using service endpoints as your title for the left nav entry while retaining the longer title as your H1 in the topic to ensure helpful search results.
IMPORTANT:
* If your service supports only service endpoints, include it in the **How to** nav group in the **Enhancing security** topic group in your `toc.yaml` file.
* If your service supports both service endpoints and VPE for VPC, then refer to the guidance about placement in a nested topic group within the Enhancing security topic group: https://test.cloud.ibm.com/docs/writing?topic=writing-security-content-guidance-->

_Make sure that you use the following title for your topic._

# Using service endpoints to privately connect to Direct Link
{: #service-endpoints}

<!--The short description should be a single, concise paragraph that contains one or two sentences and no more than 50 words. Summarize your offering's support for non-public service endpoints. You can use the following example for a service supporting the use of IBM Cloud service endpoints for network isolation:-->

To ensure that you have enhanced control and security over your data when you use Direct Link, you have the option of using private routes to {{site.data.keyword.cloud}} service endpoints. Private routes are not accessible or reachable over the internet. By using the {{site.data.keyword.cloud_notm}} private service endpoints feature, you can protect your data from threats from the public network and logically extend your private network.
{: shortdesc}

_Required: Document any customer data that goes over public routes even with the IBM Cloud service endpoints feature enabled using a connection over private routes. For example, if your service sends customer data to a data-service using a public route or sends customer logs using public routes to LogDNA that should be documented._

<!-- Work with your offering's SMEs to fill out the following sections as applicable to your offering. -->


## Before you begin
{: #prereq-service-endpoint}

_Document that users can connect to your service over a private network by using IBM Cloud private service endpoints. Point to the [core documentation](/docs/resources?topic=resources-private-network-endpoints) about how to enable the capability in their account, and then cover any details that are specific to your service about using it, for example:_

You must first enable virtual routing and forwarding in your account, and then you can enable the use of IBM Cloud private service endpoints. For more information about setting up your account to support the private connectivity option, see [Enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint).

## Setting up service endpoints for Direct Link
{: #endpoint-setup}

_Review the following example: https://cloud.ibm.com/docs/secrets-manager?topic=secrets-manager-service-connection Depending on how your service supports and requires users to set up this capability, document the steps to ensure a user can successfully connect over the private service endpoint. You can use separate headers to break this into sections if the process includes a lot of steps or use numbered steps for a less lengthy process._

High level steps typically covered are: Add a private network endpoint, view your endpoint URL, and modifying your apps to use the new endpoint.

## Disabling public service endpoints for for _servicename_
{: #endpoint-disable}

_This section will not apply to all services. It does apply to compute services, databases, and Cloud Object Storage at this time._

_Review the following example: https://cloud.ibm.com/docs/metrics-router?topic=metrics-router-service-endpoints Depending on how and if your service supports users to disable public endpoints, document the steps for disabling a public endpoint to ensure a user can connectly over only the private endpoint, if this is an option. You can use separate headers to break this into sections if the process includes a lot of steps or use numbered steps for a less lengthy process._
