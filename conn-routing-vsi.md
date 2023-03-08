---

copyright:
  years: 2020
lastupdated: "2023-02-23"

keywords: verifying, connection, connectivity

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Routing in classic virtual server instances
{: #routing-classic-vsi}

If you are attempting to access an {{site.data.keyword.cloud_notm}} classic infrastructure virtual server instance that has both a private network interface (`eth0`) and a public network interface (`eth1`), then the issue could be the traffic being routed to the public network interface versus the private. The routing tables for these interfaces point the default gateway to the public interface (`eth1`). Transit gateways are connected only to the private networks. You might have to add entries to route the subnets from other VPCs through the private interface.

## GRE tunnel connectivity issues
{: #gre-tunnel-conn-issues}

If BGP is not established over the GRE tunnel, first try pinging the BGP peer IP address to ensure layer 2 connectivity exists over the GRE tunnel.

If the BGP settings are correct, then check that the MTU setting on your device matches the MTU for the GRE gateway.

Otherwise, if BGP can utilize `OpenSent` or `OpenConfirm`, check the BGP multi-hop settings on your device. Some GRE tunnel configurations may not adjust the BGP TCP TTL. As a workaround, set your multi-hop to a value of 16, which will force the TTL value of the BGP packet to expire after 16 routed hops.
