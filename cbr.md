---

copyright:
  years:  2022
lastupdated: "2022-10-27"

keywords: CBR, context-based restrictionsb

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Protecting resources with context-based restrictions (limited availability)
{: #cbr}

Context-based restrictions give account owners and administrators the ability to define and enforce access restrictions for {{site.data.keyword.cloud}} resources based on the context of access requests. Access to Transit Gateway resources can be controlled with context-based restrictions and identity and access management policies.
{: shortdesc}

The preview of this functionality is available only to authorized accounts. 
{: preview}

These restrictions work with traditional IAM policies, which are based on identity, to provide an extra layer of protection. Unlike IAM policies, context-based restrictions don't assign access. Context-based restrictions check that an access request comes from an allowed context that you configure. Since both IAM access and context-based restrictions enforce access, context-based restrictions offer protection even in the face of compromised or mismanaged credentials. For more information, see [What are context-based restrictions](/docs/account?topic=account-context-restrictions-whatis).

A user must have the Administrator role on the Transit Gateway service to create, update, or delete rules. And a user must have either the Editor or Administrator role on the Context-based restrictions service to create, update, or delete network zones.
{: note}

Any {{site.data.keyword.cloudaccesstraillong_notm}} or audit log events generated will come from the context-based restrictions service, and not Transit Gateway. For more information, see [Monitoring context-based restrictions](/docs/account?topic=account-cbr-monitor).

To get started protecting your Transit Gateway with context-based restrictions, see the tutorial for [Leveraging context-based restrictions to secure your resources](/docs/account?topic=account-context-restrictions-tutorial). 

## Creating rules
{: #cbr-rules}

Context-based restrictions for the transit service can be scoped to a Transit Service resource type. Since the Transit Service only has one applicable resource type, it will be set to `gateway`.

Additionally, rules can be scoped to a specific instance of the service or a resource group by using resource attributes. 

### Creating rules by using the CLI
{: #cbr-rules-cli}
{: cli}

1. To create rules from the CLI, [install the CBR CLI plug-in](/docs/account?topic=cli-cbr-plugin#install-cbr-plugin).
1. Use the  [`ibmcloud cbr rule-create` command](/docs/account?topic=cli-cbr-plugin#cbr-cli-rule-create-command) to create CBR rules. For more information, see the CBR [CLI reference](/docs/account?topic=cli-cbr-plugin#cbr-zones-cli).

The examples in this section are enforcement rules. You can make them report-only by adding `--enforcement-mode report`. 

The following example CLI commands creates a context-based restriction rule for Transit Service instances in the current account:
	
* Create a disabled rule against all gateway instances in your transit service:

   ```sh
   ibmcloud cbr rule-create --description transit-rule1 --service-name transit --resource-type gateway --zone-id=<zone_id> --enforcement-mode disabled
   ```
   {: pre}

* Create a disabled rule against all gateway instances in ResourceGroup `x` in your transit service:

   ```sh
   ibmcloud cbr rule-create --description transit-rule2 --service-name transit --resource-type gateway --resource-attributes "resourceGroupId=<rg_x_id>" --zone-id=<zone_id> --enforcement-mode disabled
   ```
   {: pre}

* Create an enabled rule against the gateway instance with an ID of `y` in ResourceGroup `x` in your transit service:

   ```sh
   ibmcloud cbr rule-create --description transit-rule3 --service-name transit --resource-type gateway --resource-attributes "resource=<id_y>,resourceGroupId=<rg_x_id>" --zone-id=<zone_id> --enforcement-mode disabled
   ```
   {: pre}
   
## How Transit Gateway integrates with context-based restrictions
{: #cbr-overview}

Transit Gateway calls other services (VPC, Direct Link) when working with its connections. These other services perform the authority checks against the caller, not the Transit Gateway service. Therefore, Transit Gateway is not supported as a service reference, and does not show as a service in the **Reference a service** section when creating a network zone.
