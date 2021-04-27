---
copyright:
  years: 2021
lastupdated: "2021-04-27"

keywords: security, compliance, monitoring

subcollection: transit-gateway

---

{:external: target="_blank" .external}
{:note: .note}
{:term: .term}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}

# Managing security and compliance with IBM Cloud Transit Gateway
{: #manage-security-compliance}

{{site.data.keyword.tg_full}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}

<!--Add the following sections as your service onboards to the Security and Compliance Center. You might have only monitoring or you might also have configuration enforcement. Also, if you only have one of the options, be sure to remove the bulleted list and write the following section as a sentence.-->

With the {{site.data.keyword.compliance_short}}, you can monitor for controls and goals that pertain to {{site.data.keyword.tg_full}}.

## Monitoring security and compliance posture with IBM Cloud Transit Gateway
{: #monitor-security-compliance}

As a security or compliance focal, you can use the {{site.data.keyword.tg_full_notm}} [goals](x2117978){: term} to help ensure that your organization is adhering to the external and internal standards for your industry. By using the {{site.data.keyword.compliance_short}} to validate the resource configurations in your account against a [profile](x2034950){: term}, you can identity potential issues as they arise.

* All of the goals for {{site.data.keyword.tg_full_notm}} are added to the {{site.data.keyword.cloud_notm}} Best Practices Controls 1.0 profile, but can also be mapped to other profiles. 

* Ensure at the account-level that no cross-account requests are made via {site.data.keyword.tg_full_notm}}.

To start monitoring your resources, check out [Getting started with {{site.data.keyword.compliance_short}}](https://cloud.ibm.com/docs/security-compliance?topic-security-compliance-getting-started).

### Available goals for IBM Cloud Transit Gateway
{: #available-goals}

* Ensure at the account-level that no cross-account approvals can be done via {{site.data.keyword.tg_full}}.

## Governing IBM Cloud Transit Gateway resource configuration
{: #govern-transit}

As a security or compliance focal, you can use the {{site.data.keyword.compliance_short}} to define configuration rules for the instances of {{site.data.keyword.tg_full}} that you create.

[Config rules](#x3084914){: term} are used to enforce the configuration standards that you want to implement across your accounts. To learn more about the data that you can use to create a rule for {{site.data.keyword.tg_full}}, review the following table.

| Resource kind | Property | Operator | Value | Description |
|----|----------|-------|-------|---------------------------|
| *service* | *cross_account_connection_approved* | *is_false*<br /><br /><br /><br /><br />*is_true* | - | Indicates whether an incoming cross-account request can be approved.<br /><br />Indicates whether the final cross account connection can be deleted.|
{: caption="Table 1. Rule properties for {{site.data.keyword.tg_full}}" caption-side="top"}

To learn more about config rules, see [What is a config rule?](/docs/security-compliance?topic=security-compliance-what-is-rule).
