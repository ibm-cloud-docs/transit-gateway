---

copyright:
  years: 2020
lastupdated: "2023-02-23"

keywords: verifying, connection, connectivity

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Working with firewalls and gateway appliances
{: #firewalls-gateways}

Ensure that a firewall or gateway appliance (such as a [Juniper vSRX](/docs/vsrx?topic=vsrx-getting-started#getting-started)) is not blocking your traffic. 

For instance, the Juniper vSRX is a firewall appliance that sits between {{site.data.keyword.cloud_notm}} classic infrastructure and the BCR. If you perform a trace route and cannot get to any address at all, then it could be that the vSRX that is blocking the traffic.
