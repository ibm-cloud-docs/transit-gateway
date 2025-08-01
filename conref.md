---

copyright:
  years: 2023, 2025
lastupdated: "2025-07-25"

keywords:

subcollection: transit-gateway

content-type: conref

---

# heading 1
{: #heading-1}

## Route report considerations
{: #reuse-route-report-considerations}

* The AS path displayed in a route report provides a single zone perspective. If your source or destination spans different zones, the path length may vary. For instance, consider two direct links: one in `DAL10` and the other in `DAL12`, both advertising the same AS path length toward a `DAL`-based transit gateway connected to a VPC or classic environment. When calling from a `DAL10` virtual server instance:

   * The `DAL10` direct link is preferred.
   * For connections originating from `DAL12`, the `DAL12` direct link is preferred.
   * In the case of DAL13, you would either get ECMP routing, assuming your gateway is set up for it, or a single direct link would be used. However, during a BGP reset, it could switch to the other direct link.
* Overlapping routes are a common issue when configuring a transit gateway. If the routes from two or more connections overlap, traffic might not be routed as intended. For more information, see [Addressing route conflicts](/docs/transit-gateway?topic=transit-gateway-route-reports&interface=ui#route-conflicts).
* After a new virtual connection (VPC, Classic infrastructure, or Direct Link) reaches **Active** state, allow 5 minutes for the routes to be learned by your transit gateway. Generating a route report before all routes are learned results in a partial route report.
* If a connection exposes a route of `0.0.0.0/0`, that route is ignored when computing overlapping prefixes.
* Only one report per gateway is available at any time. If you generate a new report, the old report is deleted.
* Older route reports might be inaccurate after you add or remove a connection. As a result, if you update routes within those connections, it is recommended that you generate a new route report.
* If one or more routes are denied by [prefix filters](/docs/transit-gateway?topic=transit-gateway-adding-prefix-filters), those routes don't appear in the route report.
