---

copyright:
  years: 2020, 2024
lastupdated: "2023-02-23"

keywords: verifying, connection, connectivity

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Working with Network Interface Card routing
{: #tg-nic}

When working with a VSI that has multiple network interface cards (NICs), pay close attention to its networking settings to avoid connectivity problems. These problems may be due to how the routing works in the VSI and its security group. The default route points to the first NIC. In that case, pinging the address of the first NIC may work, however pinging the address of the second NIC may fail. Your security group may block response traffic that is not associated with inbound traffic.

As per your needs, you may need to change your default route to configure where to route traffic from all source addresses. Or, you may need to add a route to your routing table to configure where to send traffic from specific source addresses.
