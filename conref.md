---

copyright:
  years: 2023, 2025
lastupdated: "2025-02-13"

keywords:

subcollection: transit-gateway

content-type: conref

---

# heading 1
{: #heading-1}

## Route report considerations
{: #reuse-route-report-considerations}


* Overlapping routes are a common issue when configuring a transit gateway. If the routes from two or more connections overlap, traffic might not be routed as intended. For more information, see [Addressing route conflicts](/docs/transit-gateway?topic=transit-gateway-route-reports&interface=ui#route-conflicts).
* After a new virtual connection (VPC, Classic infrastructure, or Direct Link) reaches **Active** state, allow 5 minutes for the routes to be learned by your transit gateway. Generating a route report before all routes are learned results in a partial route report.
* If a connection exposes a route of `0.0.0.0/0`, that route is ignored when computing overlapping prefixes.
* Only one report per gateway is available at any time. If you generate a new report, the old report is deleted.
* Older route reports might be inaccurate after you add or remove a connection. As a result, if you update routes within those connections, it is recommended that you generate a new route report.
* If one or more routes are denied by [prefix filters](/docs/transit-gateway?topic=transit-gateway-adding-prefix-filters), those routes do not appear in the route report.
