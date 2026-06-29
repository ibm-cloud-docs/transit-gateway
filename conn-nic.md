---

copyright:
  years: 2020, 2026
lastupdated: "2026-06-29"

keywords: verifying, connection, connectivity

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Working with Network Interface Card routing
{: #tg-nic}

When working with a virtual server instance that has multiple network interface cards (NICs), pay close attention to its networking settings to avoid connectivity problems. These problems might be due to how the routing works in the virtual server instance and its security group. The default route points to the first NIC. In that case, pinging the address of the first NIC might work, however pinging the address of the second NIC might fail. Your security group might block response traffic that is not associated with inbound traffic.
{: shortdesc}

Depending on your needs, you might need to change your default route to configure where to route traffic from all source addresses. Or, you might need to add a route to your routing table to configure where to send traffic from specific source addresses.
