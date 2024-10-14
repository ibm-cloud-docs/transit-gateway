---

copyright:
  years: 2020, 2024
lastupdated: "2020-04-16"

keywords: iam, permissions

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Using IAM permissions with IBM Cloud Transit Gateway
{: #iam}

{{site.data.keyword.tg_full}} uses the IBM Cloud Identity and Access Management (IAM) platform access roles to manage access to the service's resources. IAM access roles allow account administrators to assign different levels of permission for using the service. The following tables provide the list of actions that you can take against the {{site.data.keyword.tg_full_notm}} service and its resources depending on a user's assigned roles.

## Platform-access roles
{: #platform-roles-iam}

{{site.data.keyword.tg_full_notm}} supports Administrator, Editor, Operator, and Viewer platform-access roles.

| Role | Description of Actions |  Actions |
|---|---|---|
| Administrator | Can perform all actions, including managing gateways and connections, and assign {{site.data.keyword.tg_full_notm}} IAM access policies to other users. | Create gateways  \n Delete gateways  \n Edit gateways  \n Add or remove gateway connections  \n Accept or reject a cross account connection request  \n Edit gateway connections  \n Update user access policies for the service |                     |
| Editor | Can perform all actions, including managing gateways and connections, but cannot assign {{site.data.keyword.tg_full_notm}} IAM access policies to other users. |Create gateways  \n Delete gateways  \n Edit gateways  \n Add or remove gateway connections  \n Accept or reject a cross account connection request  \n Edit gateway connections |
| Operator and Viewer | Can only perform actions that don't change the state of resources. | List gateways  \n Get gateways  \n List a gateway's connections  \n View a gateway's connections  \n View incoming connection requests |
{: caption="IAM platform-access user roles and actions" caption-side="bottom"}

To add or remove connections to VPCs, or to accept or reject a cross account connection request, you must also have Administrator or Editor platform-access role permission to the VPC being connected to. See [VPC: Getting started with IAM](/docs/vpc?topic=vpc-iam-getting-started) for more information.
{: note}

To add or remove connections to Direct Links, you must also have Administrator or Editor platform-access role permission to the Direct Link being connected to. See [Managing access for IBM Cloud Direct Link](/docs/dl?topic=dl-iam) for more information.
{: note}

## Service name
{: #transit-service-name}

The service name that you designate will vary depending on how you access IBM Cloud Transit Gateway. If you are using the IBM Cloud CLI, APIs, or Terraform, then you should use `transit` for your service name. If you are using the UI, `Transit Gateway` should be the service name.
