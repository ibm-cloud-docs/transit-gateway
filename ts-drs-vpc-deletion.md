---

copyright:
  years: 2026, 2026
lastupdated: "2026-10-21"

keywords: dynamic route server, troubleshoot, delete, VPC connection, detached, cross-account

subcollection: transit-gateway

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why can't I delete my VPC connection after removing a dynamic route server connection? (beta)
{: #troubleshoot-drs-vpc-deletion}
{: troubleshoot}
{: support}

[Dynamic Route Server for VPC is a beta feature](/docs/transit-gateway?topic=transit-gateway-transit-gateway-release-notes#transit-gateway-drs) that is available for evaluation and testing purposes to select customers. Access is restricted to allowlisted accounts.
{: beta}

After removing a dynamic route server connection, you are unable to delete the VPC connection from the transit gateway. In a cross-account scenario, the gateway owner may see the dynamic route server connection in a `Detached` state even after the network owner has removed it from their side.
{: tsSymptoms}

There is a strict ordering dependency between a dynamic route server connection and its host VPC connection:
{: tsCauses}

- The dynamic route server connection must be **fully deleted** before the VPC/Transit Gateway connection can be deleted.
- In a cross-account scenario, when the network owner deletes the dynamic route server connection from their side, the gateway owner sees the connection in a `Detached` state—not fully removed. While the connection is in `Detached` state, the underlying relationship still exists, and the VPC/Transit Gateway connection cannot be deleted by the network owner.

For more information about cross-account connection states, see [Adding cross-account connections](/docs/transit-gateway?topic=transit-gateway-adding-cross-account-connections&interface=ui).

To resolve this issue, follow the steps for your scenario:
{: tsResolve}

## Single-account scenario
{: #ts-drs-vpc-deletion-fix-single-account}

If the dynamic route server connection and the VPC connection belong to the same account:

1. Confirm that the dynamic route server connection is fully deleted. On the transit gateway connections page, verify that the connection no longer appears. If it is still present, delete it and wait for the deletion to complete before proceeding.
1. Once the dynamic route server connection is fully removed, delete the VPC/Transit Gateway connection.

## Cross-account scenario
{: #ts-drs-vpc-deletion-fix-cross-account}

If the dynamic route server connection was created across accounts (network owner and gateway owner are different accounts):

1. **Network owner:** Check whether you can still see the dynamic route server connection listed in the transit gateway connections. If the connection status shows `Detached`, it has not been fully removed from the gateway owner's side.

1. **Network owner:** Contact the gateway owner and ask them to fully delete the dynamic route server connection from their account.

1. **Gateway owner:** From the transit gateway connections page, locate the dynamic route server connection in `Detached` state and delete it. Wait for the deletion to complete.

1. **Network owner:** After the gateway owner confirms that the dynamic route server connection is fully deleted, proceed to delete the VPC/Transit Gateway connection.

If you are unable to determine which connections are blocking deletion, [contact IBM Support](/docs/transit-gateway?topic=transit-gateway-getting-help-and-support).

For more information about deletion ordering, see [Dynamic route server deletion considerations](/docs/transit-gateway?topic=transit-gateway-helpful-tips#drs-deletion-considerations).
