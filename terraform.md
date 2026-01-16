---

copyright:
  years: 2021, 2026
lastupdated: "2026-01-16"

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Setting up Terraform for {{site.data.keyword.tg_short}}
{: #terraform-setup-tgw}

Terraform on {{site.data.keyword.cloud}} enables predictable and consistent creation of {{site.data.keyword.cloud_notm}} services so that you can rapidly build complex, multi-tier cloud environments following Infrastructure as Code (IaC) principles. Similar to using the {{site.data.keyword.cloud_notm}} CLI or API and SDKs, you can automate the creation, update, and deletion of your {{site.data.keyword.tg_short}} instances by using HashiCorp Configuration Language (HCL).
{: shortdesc}

Looking for a managed Terraform on {{site.data.keyword.cloud}} solution? Try out [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started). With {{site.data.keyword.bpshort}}, you can use the Terraform scripting language that you are familiar with, but you don't have to worry about setting up and maintaining the Terraform command line and the {{site.data.keyword.cloud}} Provider plug-in. {{site.data.keyword.bpshort}} also provides pre-defined Terraform templates that you can easily install from the {{site.data.keyword.cloud}} catalog.
{: tip}

## Installing Terraform and configuring resources for {{site.data.keyword.tg_short}}
{: #install-terraform}

Before you can create an authorization by using Terraform, make sure that you have completed the following:

* Make sure that you have the [required access](/docs/transit-gateway?topic=transit-gateway-iam) to create and work with {{site.data.keyword.tg_short}} resources.
* Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
* Create a Terraform configuration file that is named `main.tf`. In this file, you add the configuration to create an authorization between services by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

1. Create a {{site.data.keyword.tg_short}} instance by using the `ibm_resource_instance` resource argument in your `main.tf` file. The {{site.data.keyword.tg_short}} resource in the following example is named `transit-gateway-1`, located in `us-south`, and is created with instance ID of `ibm_tg_gateway.new_tg_gw.id`.

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

1. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://developer.hashicorp.com/terraform/cli/init){: external}.

   ```terraform
   terraform init
   ```
   {: pre}

1. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://developer.hashicorp.com/terraform/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}

1. From the [{{site.data.keyword.cloud_notm}} resource list](/resources){: external}, select the {{site.data.keyword.keymanagementserviceshort}} instance that you created and note the instance ID.
1. Verify that the access policy is successfully assigned. For more information, see [Reviewing assigned access in the console](/docs/account?topic=account-assign-access-resources&interface=ui#review-your-access-console).

## What's next?
{: #tgw-terraform-setup-next}

Now that you successfully created your first {{site.data.keyword.tg_short}} service instance with Terraform on {{site.data.keyword.cloud_notm}}, you can visit the [{{site.data.keyword.tg_short}} Terraform registry](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/tg_gateway){: external} to perform additional tasks using Terraform.
