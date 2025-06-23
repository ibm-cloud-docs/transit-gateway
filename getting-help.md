---

copyright:
  years: 2020, 2025
lastupdated: "2025-06-20"

keywords:

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Getting help and support for {{site.data.keyword.tg_short}}
{: #getting-help-and-support}

If you experience an issue or have questions when using {{site.data.keyword.tg_full}}, you can use the following resources before you open a support case.
{: shortdesc}

* Ask a question in the [AI assistant](/docs/overview?topic=overview-ask-ai-assistant) from the console or the {{site.data.keyword.cloud_notm}} CLI.
* Review [FAQs](/docs/transit-gateway?topic=transit-gateway-faqs-for-transit-gateway) in the product documentation.
* Review [Troubleshooting](/docs/transit-gateway?topic=transit-gateway-troubleshooting-connectivity) to diagnose and resolve common issues.
* Check the status of the {{site.data.keyword.Bluemix_notm}} platform and resources by going to the [Status page](/status){: external}.
* Review [Stack Overflow](https://stackoverflow.com/search?q=transit-gateway+ibm-cloud){: external} to see whether other users ran into the same problem. If you're using the forum to ask a question, tag your question with `ibm-cloud` and `transit-gateway` so that it is seen by the {{site.data.keyword.Bluemix_notm}} development teams.

If you still can't resolve the problem, you can open a support case. For more information, see [Creating support cases](/docs/account?topic=account-open-case). And if you're looking to provide feedback, see [Submitting feedback](/docs/overview?topic=overview-feedback).

## Providing support case details for {{site.data.keyword.tg_short}}
{: #support-case-details}

To ensure that the support team has all of the details for investigating your issue to provide a timely resolution, you must provide detailed information about your issue. Review the following tips about the type of information to include in your support case for issues with {{site.data.keyword.tg_short}}.

Provide the following details:

1. Provide your transit gateway ID:

   * Run `ibmcloud tg gateways` to get the Transit Gateway ID for the transit gateway in question from the output, and then collect the output of these commands `ibmcloud tg gateway GATEWAY_ID` and `ibmcloud tg connections GATEWAY_ID`.
   * In the output of the previous command, get the connection IDs for the connections to the relevant VPCs, and if relevant, the classic infrastructure connection. Also, collect the output of the following command against each connection ID: `ibmcloud tg connection GATEWAY_ID CONNECTION_ID`.
   * Ping and trace results for connectivity issues.

2. Provide a network diagram with your specific setup. For example, see [Interconnectivity patterns](/docs/transit-gateway?topic=transit-gateway-about#patterns).
3. List your source and destination IP addresses.
