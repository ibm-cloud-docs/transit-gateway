---

copyright:
  years: 2020
lastupdated: "2020-04-16"

keywords: faq, faqs, questions, transit, gateway, vpc, direct link

subcollection: transit-gateway

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:faq: data-hd-content-type='faq'}
{:note: .note}
{:important: .important}
{:term: .term}
{:support: data-reuse='support'}

# FAQs for IBM Cloud Transit Gateway
{: #faqs-for-transit-gateway}

These frequently asked questions can help you when working with the {{site.data.keyword.tg_full}}.
{: shortdesc}

## What are the differences between IBM Cloud Transit Gateway and IBM Cloud Direct Link?
{: #differences}
{: faq}
{: support}

[IBM Cloud™ Direct Link](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl) offerings provide connectivity from an external source into a customer's {{site.data.keyword.cloud_notm}} private network. While, {{site.data.keyword.tg_full_notm}} provides connectivity between resources within a customer's {{site.data.keyword.cloud_notm}} private network.

## If I connect a classic connection to a transit gateway provisioned with local routing, does that mean I can only communicate with classic infrastructure resources that are in the same location as the transit gateway?
{: #communicate-same-resources}
A classic connection allows you to communicate with all of your global classic infrastructure resources across MZRs, even if it is connected to a transit gateway provisioned with local routing.

The routing option you choose for a transit gateway only determines what VPCs you can connect to it - local routing restricts you to connecting VPCs in the same MZR as the transit gateway, while global routing allows you to connect any VPC across the MZRs. Pick the routing option that is right for your applications - pricing is changed accordingly.

## Can I create more than one transit gateway in my account?
{: #gateway_create}
{: faq}
{: support}

You can create more than one transit gateway in your account. Each transit gateway (and its connections) are logically isolated from your other transit gateways.

## Can I create more than two connections for a given transit gateway?
{: #connections}
{: faq}
{: support}

You can connect multiple VPCs in the same region to a single transit gateway with the local routing option, and connect them across regions by using global routing. Keep in mind that all of a transit gateway's network connections are interconnected, so carefully consider all resources you want to connect. Make sure each connection receives a unique name in the gateway, and that you choose the appropriate routing type (local or global) based on the location of the connections.

## Can I connect to a VPC in another IBM Cloud account?
{: #connect-vpc-in-another-account}
{: faq}
{: support}

You can connect to a VPC in another IBM Cloud account by providing the CRN of the VPC when adding a connection to your transit gateway. The account containing the VPC is then able to view the gateway and all of its connections, and must choose to opt-in to allow account-to-account interconnectivity for that VPC. For more information see [Adding a cross-account (VPC only) connection](/docs/transit-gateway?topic=transit-gateway-edit-gateway#adding-cross-account-connections)

## How many connection requests can I make from one account to VPCs in other IBM Cloud accounts?
{: #connection-requests-account-vpcs}
{: faq}
{: support}
Each gateway is only permitted to have 10 outstanding requests for a cross account connection.

## Can I connect a VPC with generation 1 compute and a VPC with generation 2 compute using a transit gateway?
{: #gateways}
{: faq}
{: support}

You can connect any two or more VPCs (Gen 1 or Gen 2) using a transit gateway.

## I have connected a VPC to one transit gateway. Can I connect that VPC to a second transit gateway?
{: #connections-two-vpcs}
{: faq}
{: support}

You cannot connect a VPC to more than one transit gateway at a time. A given VPC can only be connected to one transit gateway in your account.

## I have connected the classic connection to one transit gateway. Can I connect the classic connection to a second transit gateway?
{: #connections-two-tg}
{: faq}
{: support}

You cannot connect a classic connection to more than one transit gateway at a time. The classic connection can only be connected to one transit gateway in your account.

## I can only provision a transit gateway in a certain set of locations on the provisioning page. Does that mean the VPC I want to connect has to be located in one of those locations?
{: #connections-locations}
{: faq}
{: support}

By enabling global routing you can connect VPCs located in different [MZRs](/docs/overview?topic=overview-locations#mzr-table) regardless of the set of locations you can provision your transit gateway in.

## What are the service limits that I need to keep in mind while using IBM Cloud Transit Gateway?
{: #service-limits-faq}
{: faq}
{: support}

The following table details the service limits for your transit gateways and connections.

| Service limit |  Default |
|---------------------------|------|
| Number of transit gateways | 5 gateways per account, 2 gateways per region |
| Number of connections per transit gateway |  10 IBM Cloud VPCs per gateway, 1 IBM Cloud classic infrastructure connection |
| Number of prefixes per connection | 15 prefixes for VPC connections, 120 prefixes for a classic connection |
{: caption="Table 1. IBM Cloud Transit Gateway service limits" caption-side="top"}

You can open a [support ticket](/docs/get-support?topic=get-support-using-avatar#using-avatar) if you need your service limits expanded.
{: tip}

## Classic access VPCs cannot be attached to a transit gateway. How can I connect and access classic resources in those VPCs?
{: #classic-resources}
{: faq}
{: support}

Although [classic access VPCs](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure) cannot be attached to a transit gateway, access to classic resources and the classic access VPC resources can be achieved by adding the classic infrastructure connection to a transit gateway. See [classic infrastructure connection considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#classic-infrastructure-connection-considerations) for further information.

## How can "VPC Peering" be achieved on IBM Cloud?
{: #vpc-peering}
{: faq}
{: support}

{{site.data.keyword.tg_full_notm}} can be used to connect multiple VPCs to each other. As such, connecting/peering two VPCs is just a part of the functionality that the transit gateway service offers. {{site.data.keyword.cloud_notm}} does not provide a standalone VPC peering service or capability.

## Can I connect a VPN or a Direct Link to a transit gateway?
{: #vpn}
{: faq}
{: support}

A VPN or Direct Link cannot be connected to a transit gateway today.

## Can I create a global transit network using the IBM Cloud Transit Gateway?
{: #global-transit}
{: faq}
{: support}

{{site.data.keyword.tg_full_notm}} enables standard IP routing between networks (for example, global VPCs) that are connected to it. Additional functionality can be added by configuring {{site.data.keyword.IBM_notm}} or third-party virtual network functions, such as VPN, NAT, and firewalls, within one or more of the interconnected networks (for instance, using the "Transit VPC" concept).

## How can I guarantee one of my clients is not going to impact the others? 
{:faq}
{: #client-impact}

Capacity management handles the overall available capacity on the transit gateway and is subject to our weekly capacity management review. When the device reaches roughly a 50% load, we augment the connectivity to the device. 
 
## What scalability options do I have for my transit gateway? Does it manage itself? How do I know if it's reaching maximum capacity?
{:faq}
{: #scalability}

The IBM Cloud infrastructure manages all transit gateways. There are no scalability options available.

## How do you prevent Distributed Denial of Service (DDoS) attacks? What restrictions do you have in place? 
{:faq}
{: #ddos}

Neither third-parties nor the internet can see your transit gateway traffic. As no critical information (such as IP router addresses) is open to anyone but you, DDoS attacks cannot bring down the network. In addition, a typical Multi-protocol Label Switching service (MPLS) uses packet filtering and applies access control lists (ACLs) to limit access. Only the ports with routing protocols from a specific area of the network can access the information.

## What are the high availability and failover mechanisms in place for my transit gateway?
{:faq}
{: #ha-fo}

The IBM Cloud infrastructure handles high availability and disaster recovery. There are no customer interactions needed.  

## How does my transit gateway handle encryption for connectivity between VPCs?
{:faq}
{: #vpc-encryption}

IBM Cloud Transit Gateway does not perform encryption, it only provides connectivity. Encryption between VPCs is your own responsibility.

It is an RFC-2547 based platform the core network and network address are 100% concealed. 

## What are the tools for monitoring the consumption of resources associated with the service, as well as the costs and the quality of the service?
{:faq}
{: #billing-usage}

IBM Cloud Transit Gateway is integrated into the [IBM Cloud usage dashboard](https://cloud.ibm.com/docs/billing-usage?topic=billing-usage-viewingusage), which provides a summary of estimated charges for all services and resources that are used per month in your organizations. This includes the number of connections and the amount of traffic flowing across your transit gateways. IBM Cloud Transit Gateway usage is billed and reported as part of the [IBM Cloud invoice process](https://cloud.ibm.com/docs/billing-usage?topic=billing-usage-managing-invoices).

## Are there notifications through email for events of unavailability of the service?
{:faq}
{: #service-unavailability-notifications}

The standard [IBM Cloud notification process](/docs/get-support?topic=get-support-viewing-notifications) is used for any maintenance events.
