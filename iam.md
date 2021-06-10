---

copyright:
  years: 2020
lastupdated: "2020-04-16"

keywords: iam, permissions

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
{:term: .term}

# Using IAM permissions with IBM Cloud Transit Gateway
{: #iam}

{{site.data.keyword.tg_full}} uses the IBM Cloud Identity and Access Management (IAM) platform access roles to manage access to the service's resources. IAM access roles allow account administrators to assign different levels of permission for using the service. The following tables provide the list of actions that you can take against the {{site.data.keyword.tg_full_notm}} service and its resources depending on a user's assigned roles.

## Platform-access roles
{: #platform-roles-iam}

{{site.data.keyword.tg_full_notm}} supports Administrator, Editor, Operator, and Viewer platform-access roles.

| Role | Description of Actions |  Actions |
|---|---|---|
| Administrator | Can perform all actions, including managing gateways and connections, and assign {{site.data.keyword.tg_full_notm}} IAM access policies to other users. | <ul><li>Create gateways</li><li>Delete gateways</li><li>Edit gateways</li><li>Add or remove gateway connections </li><li>Accept or reject a cross account connection request </li><li>Edit gateway connections</li><li>Update user access policies for the service |                     |
| Editor | Can perform all actions, including managing gateways and connections, but cannot assign {{site.data.keyword.tg_full_notm}} IAM access policies to other users. |<ul><li>Create gateways</li><li>Delete gateways</li><li>Edit gateways</li><li>Add or remove gateway connections </li><li>Accept or reject a cross account connection request </li><li>Edit gateway connections |
| Operator and Viewer | Can only perform actions that don't change the state of resources. |<ul><li>List gateways</li><li>Get gateways</li><li>List a gateway's connections</li><li>View a gateway's connections</li><li>View incoming connection requests </li></ul>|
{: caption="Table 1. IAM platform-access user roles and actions" caption-side="top"}

To add or remove connections to VPCs, or to accept or reject a cross account connection request, the user must also have Administrator or Editor platform-access role permissions to the VPC being connected to. See [VPC: Getting started with IAM](/docs/vpc?topic=vpc-iam-getting-started) for more information.
{: note}

## Service name
{: #transit-service-name}

The service name that you designate will vary depending on how you access IBM Cloud Transit Gateway. If you are using the IBM Cloud CLI, APIs, or Terraform, then you should use `transit` for your service name. If you are using the UI, `Transit Gateway` should be the service name.
