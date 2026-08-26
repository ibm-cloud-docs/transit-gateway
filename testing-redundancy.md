---

copyright:
  years: 2026
lastupdated: "2026-08-24"

keywords: redundancy, testing, BGP, GRE, failover, AS path prepending, prefix filter

subcollection: transit-gateway

---

{{site.data.keyword.attribute-definition-list}}

# Testing redundancy for Transit Gateway connections
{: #testing-redundancy}

Redundancy testing helps verify that traffic continues to flow when a path or routing session becomes unavailable. Because customer network designs vary, there is no single recommended testing method. Choose an approach that aligns with your network architecture and operational requirements.
{: shortdesc}

Before testing, verify that redundant paths are configured and operational. You can use a [route report](/docs/transit-gateway?topic=transit-gateway-route-reports) to confirm the current routing state. Monitor routing and traffic throughout the test to confirm that failover occurs as expected and that connectivity is maintained. For more information about planning redundant connections, see [Planning for IBM Cloud Transit Gateway](/docs/transit-gateway?topic=transit-gateway-helpful-tips).

## Selecting a testing method
{: #testing-redundancy-selecting-method}

The method that you choose depends on what you want to validate.

| Validation goal | Testing method |
|-----------------|----------------|
| Simulate routing peer failure | [Shut down a BGP session](#testing-redundancy-bgp-shutdown) |
| Simulate tunnel failure | [Disable a GRE tunnel](#testing-redundancy-gre-disable) |
| Test route filtering behavior | [Apply a deny-all routing policy](#testing-redundancy-deny-all) |
| Test route preference and traffic steering | [Use AS path prepending](#testing-redundancy-as-prepend) |
{: caption="Testing methods by validation goal" caption-side="bottom"}

Using more than one method can provide a more complete validation of your redundancy design.

## Shutting down a BGP session
{: #testing-redundancy-bgp-shutdown}

Administratively shut down a BGP session on one of your peer devices. This approach simulates a routing peer failure and verifies that traffic transitions to an alternate path when routes are withdrawn. For more information about BGP, see [Border Gateway Protocol](https://www.ibm.com/think/topics/border-gateway-protocol){: external}.

To shut down a BGP session, follow these steps:

1. Identify the BGP session to test.
1. Record the current routing state.
1. Shut down the BGP session.
1. Verify that traffic moves to a redundant path.
1. Restore the BGP session and confirm normal routing.

## Disabling a GRE tunnel
{: #testing-redundancy-gre-disable}

If your deployment uses GRE tunnels, disable one tunnel endpoint on your network. This approach simulates loss of the transport path and verifies that routing converges to an alternate path. For more information about GRE tunnel connections, see [Creating a redundant GRE tunnel](/docs/transit-gateway?topic=transit-gateway-redundant-gre-connection).

To disable a GRE tunnel, follow these steps:

1. Identify the tunnel to test.
1. Disable the GRE tunnel endpoint.
1. Verify that traffic transitions to a redundant path.
1. Re-enable the tunnel and confirm normal routing.

## Applying a deny-all routing policy
{: #testing-redundancy-deny-all}

Apply a temporary routing filter or policy that blocks route exchange on a BGP session. This approach allows you to test failover behavior without bringing the BGP session down.

You can apply a deny-all prefix filter directly from the {{site.data.keyword.tg_full_notm}} console. For more information, see [Adding and managing prefix filters](/docs/transit-gateway?topic=transit-gateway-adding-prefix-filters).

To apply a deny-all routing policy, follow these steps:

1. Select the BGP session to test.
1. Apply a policy or prefix filter that blocks route advertisements or acceptance.
1. Verify that traffic transitions to a redundant path.
1. Remove the policy and confirm normal routing.

## Using AS path prepending
{: #testing-redundancy-as-prepend}

Configure AS path prepending on one BGP session to make that path less preferred. This approach tests route preference and traffic steering rather than a complete path failure.

To use AS path prepending, follow these steps:

1. Select the path to make less preferred.
1. Apply AS path prepending.
1. Verify that traffic moves to the alternate path.
1. Remove the prepending configuration and confirm that routing returns to normal.
