---

copyright:
  years: 2021
lastupdated: "2021-08-12"

subcollection: transit-gateway

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:note: .note}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}


# Setting up Terraform for {{site.data.keyword.tg_short}}
{: #terraform-setup-tgw}

Terraform on {{site.data.keyword.cloud}} enables predictable and consistent provisioning of {{site.data.keyword.cloud_notm}} services so that you can rapidly build complex, multi-tier cloud environments following Infrastructure as Code (IaC) principles. Similar to using the {{site.data.keyword.cloud_notm}} CLI or API and SDKs, you can automate the provisioning, update, and deletion of your {{site.data.keyword.tg_short}} instances by using HashiCorp Configuration Language (HCL).
{: shortdesc}

Looking for a managed Terraform on {{site.data.keyword.cloud}} solution? Try out [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started). With {{site.data.keyword.bpshort}}, you can use the Terraform scripting language that you are familiar with, but you don't have to worry about setting up and maintaining the Terraform command line and the {{site.data.keyword.cloud}} Provider plug-in. {{site.data.keyword.bpshort}} also provides pre-defined Terraform templates that you can easily install from the {{site.data.keyword.cloud}} catalog.
{: tip}

## Installing Terraform and configuring resources for {{site.data.keyword.tg_short}}
{: #install-terraform}

Before you begin, make sure that you have the [required access](/docs/transit-gateway?topic=transit-gateway-iam) to create and work with {{site.data.keyword.tg_short}} resources.

1. Follow the [Terraform on {{site.data.keyword.cloud}} getting started tutorial](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started) to install the Terraform CLI and configure the {{site.data.keyword.cloud}} Provider plug-in for Terraform. The plug-in abstracts the {{site.data.keyword.cloud}} APIs that are used to provision, update, or delete {{site.data.keyword.tg_short}} service instances and resources.
1. Create a Terraform configuration file that is named `main.tf`. In this file, you add the configuration to create a {{site.data.keyword.tg_short}} service instance and to assign a user an access policy in Identity and Access Management (IAM) for that instance by using HashiCorp Configuration Language (HCL). For more information, see the [Terraform documentation](https://www.terraform.io/docs/language/index.html){: external}.

   The {{site.data.keyword.tg_short}} resource in the following example is named `transit-gateway-1`, located in `us-south`, uses global routing, and is assigned to  `30951d2dff914dafb26455a88c0c0092`, the resource group where the transit gateway is being created.

   For more information about arguments and attributes, see the [`ibm_tg_gateway`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/tg_gateway){: external} usage example.
   {: note}

   ```terraform
   resource "ibm_tg_gateway" "new_tg_gw" {
       name="transit-gateway-1"
       location="us-south"
       global=true
       resource_group="30951d2dff914dafb26455a88c0c0092"
   }  
      
   resource "ibm_iam_user_policy" "policy" {
       ibm_id = "user@ibm.com"
       roles  = ["Administrator"]
       resources {
         service              = "transit"
         resource_instance_id = "ibm_tg_gateway.new_tg_gw.id"
       }
   }
   ```

1. Initialize the Terraform CLI.

   ```sh
   terraform init
   ```
   {: codeblock]

1. Create a Terraform execution plan. The Terraform execution plan summarizes all the actions that need to be run to create the {{site.data.keyword.tg_short}} instance in your account.

   ```sh
   terraform plan
   ```
   {: codeblock]

1. Create the {{site.data.keyword.tg_short}} instance and IAM access policy in {{site.data.keyword.cloud_notm}}.

   ```sh
   terraform apply
   ```
   {: codeblock]

1. From the [{{site.data.keyword.cloud_notm}} resource list](/resources){: external}, select the {{site.data.keyword.tg_short}} instance that you created and note the instance ID.

1. Verify that the access policy is successfully assigned. For more information, see [Reviewing assigned access in the console](/docs/account?topic=account-assign-access-resources#review-your-access-console).
