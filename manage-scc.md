---
copyright:
  years: 2021, 2022
lastupdated: "2022-06-17"

keywords: security, compliance, monitoring

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Managing security and compliance with IBM Cloud Transit Gateway
{: #manage-security-compliance}

{{site.data.keyword.tg_full}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}

With the {{site.data.keyword.compliance_short}}, you can monitor for controls and goals that pertain to {{site.data.keyword.tg_full}}.

## Monitoring security and compliance posture with IBM Cloud Transit Gateway
{: #monitor-security-compliance}

As a security or compliance focal, you can use the {{site.data.keyword.tg_full_notm}} [goals](x2117978){: term} to help ensure that your organization is adhering to the external and internal standards for your industry. By using the {{site.data.keyword.compliance_short}} to validate the resource configurations in your account against a [profile](x2034950){: term}, you can identity potential issues as they arise.

All of the goals for {{site.data.keyword.tg_full_notm}} are added to the {{site.data.keyword.cloud_notm}} Control Library, but can also be mapped to other profiles.
{: note}

To start monitoring your resources, check out [Getting started with {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic-security-compliance-getting-started).

### Available goals for IBM Cloud Transit Gateway
{: #available-goals}

* Check whether {{site.data.keyword.tg_short}} allows no cross account connection requests at the account level
* Check whether {{site.data.keyword.tg_short}} allows no cross account connection approvals at the account level

## Governing IBM Cloud Transit Gateway resource configuration
{: #govern-transit}

As a security or compliance focal, you can use the {{site.data.keyword.compliance_short}} to define configuration rules for the instances of {{site.data.keyword.tg_full}} that you create.

[Config rules](#x3084914){: term} are used to enforce the configuration standards that you want to implement across your accounts. To learn more about the data that you can use to create a rule for {{site.data.keyword.tg_full}}, review the following table.

| Resource kind | Property | Operator | Value | Description |
|----|----------|-------|-------|---------------------------|
| _service_ | _cross_account_connection_approved_ | _is_false_ \n _is_true_ | -- | Indicates whether an incoming cross account connection request can be approved. |
{: caption="Table 1. Rule properties for {{site.data.keyword.tg_full}}" caption-side="bottom"}

To learn more about config rules, see [What is a config rule?](/docs/security-compliance?topic=security-compliance-what-is-governance)
