---

copyright:
  years: 2020, 2024
lastupdated: "2024-06-11"

keywords: verifying, connection, connectivity

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Routing in classic virtual server instances and bare metal servers
{: #routing-classic-vsi}

If you are attempting to access an {{site.data.keyword.cloud_notm}} classic infrastructure virtual server instance or a bare metal server that has both a private network interface (`eth0`) and a public network interface (`eth1`), then the issue could be the traffic being routed to the public network interface versus the private. The routing tables for these interfaces point the default gateway to the public interface (`eth1`). Transit gateways are connected only to the private networks. You might have to add entries to route the subnets from other VPCs through the private interface.
