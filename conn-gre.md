---

copyright:
  years: 2020, 2024
lastupdated: "2024-06-02"

keywords: verifying, connection, connectivity

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# GRE tunnel connectivity issues
{: #gre-tunnel-conn-issues}

If you experience a connectivity issue, follow these steps to help resolve the issue:

1. If BGP is not established over the GRE tunnel, first try pinging the BGP peer IP address to ensure layer 2 connectivity exists over the GRE tunnel.
1. Verify BGP hold timer and keepalive configurations. The hold timer should be set to 90 seconds while the keepalive should be set to 30 seconds.
1. If the BGP settings are correct, then check that the MTU setting on your device matches the MTU for the GRE gateway.

   Otherwise, if BGP can utilize `OpenSent` or `OpenConfirm`, check the BGP multi-hop settings on your device. Some GRE tunnel configurations might not adjust the BGP TCP TTL. As a workaround, set your multi-hop to a value of `64`, which forces the TTL value of the BGP packet to expire after 16 routed hops.

1. For Juniper vSRX, BGP stale-routes-time is 5 minutes by default. The stale-routes-time statement allows us to set the length of time that the routing device waits to receive messages from restarting neighbors before declaring them down. In case of GRE HA failover to a second GRE, the traffic takes 5 minutes to be reflected by the second tunnel.
