---

copyright:
  years: 2020, 2024
lastupdated: "2020-06-15"

keywords: data encryption, data storage, bring your own keys, BYOK, key management, key encryption, personal data, data deletion for, data, data security

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Securing your data in IBM Cloud Transit Gateway
{: #mng-data}

Data about your specific {{site.data.keyword.tg_full}} configuration is encrypted in transit and at rest. Transit gateway configuration data is deleted upon your request through API or the user interface.
{: shortdesc}

{{site.data.keyword.tg_full_notm}} does not store any customer data. Data transmitted through a transit gateway is not encrypted by IBM.
{: note}

## How your data is stored and encrypted
{: #data-storage}

All interaction with {{site.data.keyword.tg_full_notm}} from clients is encrypted. For example, when you use an API or interact with the service through the user interface to configure gateways and connections, all such interactions are fully end-to-end encrypted. Likewise, data elements related to the your configuration are encrypted in transit and at rest. No personal or sensitive data is stored, processed, or transmitted, and data at rest is stored in an encrypted database.

However, the purpose of {{site.data.keyword.tg_full_notm}} is to join your networks together. Once one VPC is connected to another, the encryption of data that you choose to transmit across the network is your responsibility.

## Protecting your sensitive data
{: #data-encryption}

Data related to {{site.data.keyword.tg_full_notm}}'s configuration is not considered sensitive data. The configuration data is encrypted at rest at database level. The transit gatewat does not manage any customer-managed keys. As a result, there is no need or use for either Key Protect or Hyper Protect Crypto Services.

### About customer-managed keys
{: #about-encryption}

{{site.data.keyword.tg_full_notm}} does not manage any customer-managed keys. As a result, there is no need or use for either Key Protect or Hyper Protect Crypto Services.

### Enabling customer-managed keys
{: #using-byok}

{{site.data.keyword.tg_full_notm}} does not manage any customer-managed keys. As a result, there is no need or use for either Key Protect or Hyper Protect Crypto Services.

### Working with customer-managed keys
{: #working-with-keys}

{{site.data.keyword.tg_full_notm}} does not manage any customer-managed keys. As a result, there is no need or use for either Key Protect or Hyper Protect Crypto Services.

## Deleting your data in IBM Cloud Transit Gateway
{: #data-delete}

You can delete your transit gateway's configuration through API or with the user interface.

### Deleting IBM Cloud Transit Gateway instances
{: #service-delete}

You can delete your transit gateway's configuration through API or with the user interface.

### Restoring deleted data for IBM Cloud Transit Gateway
{: #data-restore}

{{site.data.keyword.tg_full_notm}} does not support the restoration of deleted data.
