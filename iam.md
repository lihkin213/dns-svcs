---

copyright:

  years: 2019

lastupdated: "2019-12-06"

keywords: dns, dns-svcs, DNS Services, Private DNS, dns vpc, Access Control Lists, IAM, permitted networks

subcollection: dns-svcs

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Managing IAM and {{site.data.keyword.dns_full_notm}}
{: #iam}

{{site.data.keyword.dns_full_notm}} is in Experimental Release. At this time the service is available to whitelisted customers only. 
{: important}

{{site.data.keyword.dns_full}} leverages IAM to perform authorization and Authentication.

Access to service name service instances for users in your account is controlled by {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). Every user that accesses the service name service in your account must be assigned an access policy with an IAM role defined. The policy determines what actions a user can perform within the context of the service or instance that you select. The allowable actions are customized and defined by the {{site.data.keyword.cloud_notm}} service as operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles.

Policies enable you to grant access at different levels. Some of the options include the following:

- Access across all instances of the service in your account.
- Access to an individual service instance in your account.
- Access to a specific resource within an instance.

## Working with permitted network (VPC) related IAM access

To add or remove a permitted network (VPC) to the DNS zone, a user must have at least `Operator` level access to all Resource Types in VPC Infrastructure Services. To provide `Operator` level access to the VPC, follow these steps:

1. Go to `cloud.ibm.com`.
1. Click the **Manage** menu list, and select **Access (IAM)**.
1. Click **Access groups** in the left navigation menu.
1. Click **Create**.
1. Enter a Name and Description in the window that appears, and then click **Create**.
1. Click **Access policies** and then click **Assign access**.
1. Click **Assign access to resources**.
1. Select **VPC Infrastructure Services** in the Services list menu.
1. Select **All resource types** in the Resource Type list menu.
1. Check the **Operator** checkbox in the Platform access list.
1. Select **Users** in the left navigation menu.
1. Click **Invites users**. 
1. Enter the user's email address in the input box.
1. Click **Add** in the row for the Access group you created, and then click **Invite**.

This provides the user with `Operator` level access to add or remove a permitted network to the DNS zone.


