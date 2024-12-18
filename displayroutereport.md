---

copyright:
  years: 2020, 2024
lastupdated: "2024-12-18"

keywords: route, report

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Generating a route report
{: #route-reports}

You can request a report of all routes known to a transit gateway and each of its connections. The report shows  Border Gateway Protocol (BGP) information associated with these routes, which connections supply which routes, and overlapping routes.

You can retrieve a route report by using the UI, CLI, or API.

{{site.data.content.reuse-route-report-considerations}}

## Generating and viewing a route report in the UI
{: #generate-route-report-ui}
{: ui}

A route report generates data for both the **Routes** and **BGP** tables in the respective views. Both of these tables allow you to generate, delete, and download the same report.
{: note}

To generate a route report in the UI, follow these steps:

1. From your browser, open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and log in to your account.
1. Select the Navigation Menu ![Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure** > **Network** > **Transit Gateway**.
1. From the Transit Gateway table, select the gateway for which you want to generate the report.
1. On the Details page, click either the **Routes** or **BGP** tab, then click **Generate report**.

   The route report begins building, and might take a few minutes to generate depending on the complexity of the gateway. Keep in mind that you cannot generate another report until the report is finished processing, or unless you click **Cancel**.

After the report generates, the following columns are displayed in the route report table.

In the Routes view:

* Route - Specifies the route address (for example, `169.254.0.40/29`).
* Connection - Specifies the name (or ID) of the specific connection that the route originated from.
* Conflict - Specifies whether or not there is a route conflict.

In the BGP view:

* Route - Specifies the route address (for example, `169.254.0.40/29`).
* Connection - Specifies the name (or ID) of the specific connection that the route originated from.
* Type - Specifies the route type: VPC, Classic infrastructure, or Direct Link.
* Local preference - Used to choose the best outbound path. Applied on inbound external routes.
* AS Path - Lists autonomous systems through which the routing information has passed. For example, `(65201 4201065540) 4203065540`.

## Generating and viewing a route report from the CLI
{: #generate-route-report-cli}
{: cli}

To generate and view a route report from the CLI, run the following command:

```sh
ibmcloud tg route-report-create|rrc GATEWAY_ID [--output json] [-h, --help]
```
{: pre}

Where:

* **GATEWAY_ID** is the ID of the gateway to list route reports for.
* **--output json** formats the output in JSON.
* **--help | -h** gets help on this command.

For example, to create a route report for a gateway:

```sh
ibmcloud tg rrc $gateway
```
{: pre}

## Generating and viewing a route report with the API
{: #generate-route-report-api}
{: api}

To generate and view a route report with the API, follow these steps:

1. Set up your [API environment](/docs/transit-gateway?topic=transit-gateway-set-up-environment) with the right variables.
1. Store any additional variables to be used in the API commands, for example:

   ```sh
   transit_gateway="11111111-b540-4766-a196-14368f328eb2"
   ```
   {: pre}

1. Request report creation:

   ```sh
   curl -X POST "$transit_api_endpoint/v1/transit_gateways/$transit_gateway/route_reports?version=$api_version" -H "Authorization: $iam_token"
   ```
   {: pre}

   For the rest of the calls, you'll need to know the ID of the newly created report. Save the ID in a variable, for example:

   ```sh
   route_report="22222222-c540-4766-a196-14368f328eb2"
   ```
   {: pre}

   To verify that the variable was saved, run `echo $route_report` and make sure the response is not empty.

1. Wait for the report to become active, then you can view its details:

   ```sh
   curl -X GET "$transit_api_endpoint/v1/transit_gateways/$transit_gateway/route_reports/$route_report?version=$api_version" -H "Authorization: $iam_token"
   ```
   {: pre}

## Addressing route conflicts
{: #route-conflicts}

Conflicting routes can cause errors, which you can see in the **Conflict** column of the **Routes** view.

Conflicting routes are not dropped from routing tables. Any conflicts that you see in the **Conflict** column are presented merely for information, so that you can easily spot potential problems in your routing, and decide how to address them, if at all. Overlapping routes may also be intentional, such as for HA purposes.
{: important}

If there are multiple conflicts, click the link to open a side panel with more information. After you resolve the conflicts, generate a new report.

When diagnosing conflicting routes, keep in the mind the following traffic flow considerations:

* If the advertised prefixes match exactly, or have the same prefix length and AS Path length, the route preferred by the BGP protocol on the IBM Cloud router is non-deterministic and might change over time. Therefore, you might expect to see routes working as expected, and then suddenly not. In a redundant GRE or Direct Link situation, this can be fine, but if you have stateful firewalls, this can be an issue in that the return path to a customer site (or virtual router) can shift if the preferred route changes.
* If the prefix lengths of two routes are different (for example, `192.168.0.0/16` and `192.168.0.0/24`), the more precise prefix is preferred. In this example, the connection advertising the `/24` prefix would be used for all matching IPs.
* If routes have the same prefix length, but different AS Paths, then the shorter AS Path is the preferred route. The prefix length takes precedence over the AS Path.
