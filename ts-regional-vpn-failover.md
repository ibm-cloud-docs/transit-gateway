---

copyright:
  years: 2026, 2026
lastupdated: "2026-08-31"

keywords: VPN gateway, regional VPN, failover, zone failure, traffic, troubleshoot

subcollection: transit-gateway

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

[New]{: tag-new}
<regional>

# Why is traffic not failing over after a zone failure on my regional VPN connection?
{: #troubleshoot-regional-vpn-failover}
{: troubleshoot}
{: support}

## What's happening
{: #ts-regional-vpn-failover-symptom}

After a zone becomes unavailable, traffic through a regional VPN gateway connection to a transit gateway stops flowing. You expect traffic to automatically shift to the VPN appliance in the healthy zone, but connectivity is not restored.

## Why it's happening
{: #ts-regional-vpn-failover-cause}

A regional VPN gateway provides automatic failover through BGP. When a VPN appliance in one zone fails, its BGP sessions with the transit gateway are withdrawn and traffic shifts to the appliance in the healthy zone. This process takes time to complete (BGP convergence time, typically a few seconds to under a minute).

If traffic is not recovering, possible causes are:

- **BGP convergence is still in progress.** Failover is not instant. Allow a short period for BGP sessions to be withdrawn and for the healthy appliance to take over routing.
- **The on-premises device is still sending traffic to the failed appliance.** If the on-premises VPN device has not yet received the BGP withdrawal, it may continue routing to the unavailable appliance until the session times out.
- **GRE enhanced route propagation is not enabled.** For traffic to continue flowing across the transit gateway connections after failover, GRE enhanced route propagation must be enabled on the transit gateway. Without it, the healthy VPN appliance's tunnels may not be able to propagate routes to all connected networks.
- **Both VPN members are in the same zone.** If the two VPN members were provisioned with subnets in the same zone, a failure of that zone takes down both appliances. Failover requires the two members to be in different zones.

## How to fix it
{: #ts-regional-vpn-failover-fix}

1. Wait a short time and recheck connectivity. BGP convergence typically completes within seconds to under a minute after a zone failure. If connectivity resumes, no further action is needed.

1. Verify that the two VPN members are in different zones. On the VPN gateway details page, check the zone for each member. If both members are in the same zone, they cannot provide zone-level failover. To correct this, update one member's subnet to a subnet in a different zone.

1. Verify that **GRE enhanced route propagation** is enabled on your transit gateway:

   1. Open the [{{site.data.keyword.cloud_notm}} console](/login){: external} and navigate to **Infrastructure** > **Network** > **Transit Gateway**.
   1. Click your transit gateway name, then click **Actions** > **Edit**.
   1. Confirm that the **GRE enhanced route propagation** toggle is enabled.

   If it is not enabled, turn it on. Review [GRE enhanced route propagation considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#gre-enhanced-route-propagation-considerations) before making this change in a production environment.

1. Check the health of the on-premises BGP session. If your on-premises device has not withdrawn the failed tunnel from its routing table, wait for the BGP hold timer to expire or manually clear the BGP session.

1. If the connection status shows `error` after the zone failure, the transit gateway may need to refresh its connection to the VPN gateway. Contact [IBM Support](/docs/transit-gateway?topic=transit-gateway-getting-help-and-support) to request a connection refresh.

For more information, see [Regional VPN gateway considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#regional-vpn-connection-considerations).

</regional>
