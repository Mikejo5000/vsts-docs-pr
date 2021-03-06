---
title: Troubleshoot permissions and access with Azure Active Directory (Azure AD)
description: Need to understand Azure AD groups, how to add users, or how to connect or disconnect to and from your directory? Read these frequently asked questions.
ms.prod: devops
ms.technology: devops-accounts
ms.assetid: d51de748-c53e-4468-ad9b-275d6bf1a4dd
ms.topic: conceptual
ms.manager: douge
ms.author: chcomley
author: chcomley
ms.date: 02/27/2018
monikerRange: 'vsts'
---

# Troubleshoot access with Azure Active Directory (Azure AD)

[!INCLUDE [version-vsts-only](../../_shared/version-vsts-only.md)]

## General

### I made changes to Azure Active Directory (Azure AD), but they didn't seem to take effect.

Changes made in Azure AD may take up to 24 hours to be visible in VSTS.

<a name="o365aad"></a>

### Can I use Office 365 and Azure AD with VSTS?

Yes. You can't do this, however, by using the [free subscription](https://technet.microsoft.com/library/dn832618.aspx)
that you can activate when you connect Office 365 and Azure AD.

Instead, you must [sign up for a new Azure subscription](https://azure.microsoft.com/pricing/purchase-options/). You can also use an existing Azure subscription
that's not from one of these offers:

* An [Azure free trial](https://azure.microsoft.com/offers/ms-azr-0044p/)

* A [free Azure AD subscription](https://technet.microsoft.com/library/dn832618.aspx)

You must then associate that subscription with your Office 365 connection to Azure AD. Note that you need additional subscription administrator permissions, beyond the co-administrator permissions.

Learn how to [associate your Azure subscription to Azure AD](https://docs.microsoft.com/azure/billing-add-office-365-tenant-to-azure-subscription).

<a name="ChooseOrgAcctMSAcct"></a>

[!INCLUDE [choose-msa-azuread-account](../../_shared/qa-choose-msa-azuread-account.md)]

[!INCLUDE [choose-msa-azuread-account2](../../_shared/qa-choose-msa-azuread-account2.md)]

<a name="ChangeMSA"></a>

### My organization uses Microsoft accounts only. Can I switch to Azure AD?

Yes, but before you switch, make sure that Azure AD meets your needs for sharing work items, code, resources, and other assets with your team and partners.

Learn more about the differences in how you
[control access with Microsoft accounts or with Azure AD, and how to switch when you're ready](access-with-azure-ad.md).

[!INCLUDE [find-organization-owner](../../_shared/qa-find-organization-owner.md)]

[!INCLUDE [why-no-owned-organizations](../../_shared/qa-why-no-owned-organizations.md)]

[!INCLUDE [why-cant-sign-in-msa-azuread-account](../../_shared/qa-why-cant-sign-in-msa-azuread-account.md)]

## Understand Azure AD groups

### Why can't I assign VSTS permissions directly to an Azure AD group?

Because these groups are created and managed in Azure, you can't assign VSTS permissions directly or secure version control paths to these groups. You'll get an error if you try to assign permissions directly.

You can add an Azure AD group to the VSTS group that has the permissions you want. Or,
you can assign these permissions to the VSTS group instead. Azure AD group members inherit permissions from the VSTS group where you add them.

### Can I manage Azure AD groups in VSTS?

No, because these groups are created and managed in Azure. VSTS doesn't store or sync member status for Azure AD groups. To manage Azure AD groups, use the [Azure portal](https://portal.azure.com), Microsoft Identity Manager (MIM), 
or the group management tools that your organization supports.

### How do I tell the difference between a VSTS group and an Azure AD group?

On the group's identity card, check the group's source.

![Screenshot of group identity card](_img/manage-azure-ad-groups/checkidentitysourceaad.png)

### Why doesn't the Users hub show all Azure AD group members?

These users have to sign in to your VSTS organization before they appear in the Users hub. 

<a name="AssignLicenses"></a>

### How do I assign organization access to Azure AD group members?

When these group members sign in to your VSTS organization for the first time, VSTS assigns an access level to them automatically. If they have
[Visual Studio subscriptions](faq-add-delete-users.md#EligibleMSDNSubscriptions),
VSTS assigns the respective access level to them. Otherwise, VSTS assigns them the next "best available"
[access level](https://visualstudio.microsoft.com/pricing/visual-studio-online-feature-matrix-vs), in this order: Basic, Stakeholder.
 
If you don't have enough access levels for all Azure AD group members, those members who sign in will get a Stakeholder access.

### Why doesn't the Security tab show all members when I select an Azure AD group?

The Security tab shows Azure AD group members only after they sign in to your VSTS organization, and have an access level assigned to them.

To see all Azure AD group members, use the [Azure portal](https://portal.azure.com), Microsoft Identity Manager (MIM), or the group management tools that your organization supports.

### Why doesn't the team members widget show all Azure AD group members?

The team members widget shows only users who previously signed in to your VSTS organization.

### Why doesn't the team capacity pane show all Azure AD group members?

The team capacity pane shows only users who previously signed in to your VSTS organization.
To set capacity, manually add users to your team.

### Why doesn't the team room show offline users?

The team room shows Azure AD group members, but only when they're online.

### Why doesn't VSTS reclaim access levels from users who aren't Azure AD group members anymore?

VSTS doesn't automatically reclaim access levels from these users. To manually remove their access, go to the **Users** hub.

### Can I assign work items to Azure AD group members who haven't signed in?

You can assign work items to any Azure AD member who has permissions for your VSTS organization. This also adds that member to your VSTS organization. When you add users this way, they'll automatically appear in the Users hub, with the best available
access level. They'll also appear in the security settings.

### Can I use Azure AD groups to query work items by using the "In Group" clause?

No, querying on Azure AD groups is unsupported.

### Can I use Azure AD groups to set up field rules in my work item templates?

No, but you might be interested in our [process customization plans](https://blogs.msdn.com/b/visualstudioalm/archive/2015/07/27/visual-studio-online-process-customization-update.aspx).

<a name="remove-user-azure-ad-group"></a>

### Why am I asked to remove a user from an Azure AD group when I delete that user from my VSTS organization?

Users can belong to your VSTS organization, both as individuals and as members of Azure AD groups that were added to VSTS groups. These users can still access your VSTS organization while they're members of these Azure AD groups.

To block all access for these users, remove them from Azure AD groups in your VSTS organization, or remove these groups from your VSTS organization. Although we'd like to make it possible to block access completely or make exceptions for such users, VSTS doesn't currently have this capability.

### How do I remove an Azure AD group from VSTS?

Go to your team project collection or team project. In the bar at the top, select the gear icon, and then select **Security**.

Find the Azure AD group, and delete it from your VSTS organization.

![Screenshot of team project, with Delete option highlighted](_img/manage-azure-ad-groups/deleteaadgroupfromvso.png)

<a name="ChooseOrgAcctMSAcct"></a>

[!INCLUDE [why-cant-sign-in-msa-azuread-account](../../_shared/qa-why-cant-sign-in-msa-azuread-account.md)]

<a name="faq-users"></a>

## Add users to directory

### Can I switch current users from Microsoft accounts to work accounts in VSTS?

No. Although you can add new work accounts to your VSTS organization, they're treated as new users. If you want to access all your work, including its history, you must use the same sign-in addresses that you used before your VSTS organization was connected to your Azure AD.
You can do this by adding your Microsoft account as a member to your Azure AD.

### Why can't I add users from other directories to my Azure AD?

You must be a member or have read access in those directories. Otherwise, you can add them
[using B2B collaboration through your Azure AD administrator](https://azure.microsoft.com/documentation/articles/active-directory-b2b-collaboration-overview/). You can also add them by using their Microsoft accounts, or by creating new work accounts for them in your directory.

### How do I use my work or school account with my Visual Studio with MSDN subscription?

If you used a Microsoft account to activate a [Visual Studio with MSDN subscription](https://visualstudio.microsoft.com/vs/pricing/) that includes VSTS as a benefit, you can add a work or school account. The account must be managed by Azure AD. Learn [how to link work or school accounts to Visual Studio with MSDN subscriptions](../../billing/link-msdn-subscription-to-organizational-account-vs.md).

<a name="guest-access"></a>

### Can I control access to my VSTS organization for external users in the connected directory?

Yes, but only for external users who are [added as guests through Office 365](https://support.office.com/article/Share-sites-or-documents-with-people-outside-your-organization-80E49744-E30F-44DB-8D51-16661B1D4232)
or [added using B2B collaboration by your Azure AD administrator](https://azure.microsoft.com/documentation/articles/active-directory-b2b-collaboration-overview/). These external users are managed outside the connected directory. To learn more, contact your Azure AD administrator. The following setting doesn't affect [users who are added directly to your organization's directory](https://azure.microsoft.com/documentation/articles/active-directory-create-users/).

Before you start, make sure you have at least Basic access, not Stakeholder.

#### To control organization access for external users added through Office 365 or Azure AD B2B collaboration

1. Go to your VSTS organization's control panel.

   ![Screenshot of team project with gear icon highlighted](_img/_shared/OrganizationSettings.png)

2. Go to your organization settings.

   Allow or deny organization access for external users added as guests.

   ![Screenshot of organization settings](_img/manage-work-access/guest-access.png)

<a name="faq-connect"></a>

## Connect to directory

<a name="connect-o365-azure-ad"></a>

### Can I connect my VSTS organization to an Azure AD created from Office 365?

Yes. If you can't find your Azure AD created from Office 365, see
[Why don't I see the directory that I want to connect?](#why-not-my-directory).

<a name="no-directory-subscription"></a>

### Why don't I see a directory associated with my Azure subscription?

To make your directory appear in the Azure portal, you need an active and valid ["full" Azure subscription](https://azure.microsoft.com/pricing/purchase-options/), such as a ["Pay-As-You-Go" subscription](https://azure.microsoft.com/offers/ms-azr-0003p/). This subscription should be associated with your organization's Azure AD, and you need at least co-administrator permissions for your subscription.

With these, you can link your subscription and connect your Azure AD to your VSTS organization. Learn [how to manage Azure subscription administrators](../billing/add-backup-billing-managers.md).

<a name="why-not-my-directory"></a>

### Why don't I see the directory that I want to connect? What should I do?

This might happen because:

* You don't have [VSTS organization owner permissions](faq-change-app-access.md#find-owner) to manage directory connections.

* You don't have an active and valid ["full" Azure subscription](https://azure.microsoft.com/pricing/purchase-options/) associated with your organization's Azure AD. (This problem is described in the preceding question.) 

  For example, if you want to use an Azure AD created from Office 365,
  you can't use the [free subscription](https://technet.microsoft.com/library/dn832618.aspx)
  option. You must [sign up for a new Azure subscription](https://azure.microsoft.com/pricing/purchase-options/), or use an existing Azure subscription. The existing Azure subscription can't be one of the following offers:

  * An [Azure free trial](https://azure.microsoft.com/offers/ms-azr-0044p/)
  * A [free Azure AD subscription](https://technet.microsoft.com/library/dn832618.aspx)

  You must then associate that subscription with your Azure AD created from Office 365. To do this, you'll need additional subscription administrator permissions, beyond co-administrator permissions. Learn how to [associate your Azure subscription to your Office 365 Azure AD](https://docs.microsoft.com/azure/billing-add-office-365-tenant-to-azure-subscription),
  or learn more about the [relationship between your Azure subscription and your Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-how-subscriptions-associated-directory#how-an-azure-subscription-is-related-to-azure-ad).

<a name="remove-spending-limit"></a>

* Your VSTS organization isn't linked to the Azure subscription that's associated with your directory. Learn [how to link them](../billing/set-up-billing-for-your-organization-vs.md).

  >[!IMPORTANT]
  This link also sets up organization billing, so you can bill VSTS purchases to your Azure subscription. Some Azure subscriptions have a [spending limit](https://azure.microsoft.com/pricing/spending-limits/). If your Azure subscription has a spending limit, and you want to bill purchases to this subscription, you must remove this limit indefinitely. This prevents disabling your Azure subscription the
  next month when your monthly charges are billed. Otherwise, all resources billed to this subscription will be suspended, including all VSTS purchases, Visual Studio Marketplace purchases, and Azure resources. Learn more about [how to manage your subscription's spending limit](https://msdn.microsoft.com/library/azure/dn465781.aspx).

  If you're the [organization administrator](https://azure.microsoft.com/documentation/articles/billing-add-change-azure-subscription-administrator) for the subscription, visit the Azure Account Center to remove the spending limit:

  1. Sign in to the [Azure portal](https://portal.azure.com), and go to the Azure Account Center (**Account** > **subscriptions**).
  2. Select your Azure subscription. 
  3. Remove your spending limit **indefinitely**.

<a name="subscription-linked-already"></a>

### What if my VSTS organization is already linked to an Azure subscription?

You can [change the Azure subscription](../billing/change-azure-subscription.md) that's linked to your VSTS organization. Note that unlinking causes your organization to revert to the free tier. For details, see the [VSTS billing FAQ](../billing/vsts-billing-faq.md).

### What happens if I unlink my Azure subscription while my VSTS organization is connected to a directory?

See the [VSTS billing FAQ](../billing/vsts-billing-faq.md).

<a name="AlreadyConnected"></a>

### Why is my VSTS organization already connected to a directory? Can I change that directory?

Your VSTS organization was connected to a directory when the organization owner created the organization, or sometime after that. When you create a VSTS organization with a work or school account, your VSTS organization is automatically connected to the directory that manages that work or school account. You can [disconnect your VSTS organization](disconnect-organization-from-aad.md) from this directory, and reconnect to another directory. You might have to migrate some users.

<a name="AlternateCredentials"></a>

### My alternate credentials don't work anymore. What do I do?

This happens after you connect your VSTS organization to a directory. You must
[set up your credentials](http://support.microsoft.com/kb/2991274) again for the organization that you connected.

<a name="CantSignIn"></a>

### Why can't users sign in after my VSTS organization is connected to a directory?

Make sure their sign-in addresses are in the connected directory, and in your VSTS organization. If they're not directory members, and you have at least [user administrator permissions](https://azure.microsoft.com/documentation/articles/active-directory-assign-admin-roles/),
you can [add them to the directory](https://azure.microsoft.com/documentation/articles/active-directory-create-users/).

Some users have sign-in addresses that are shared by their Microsoft account and their work or school account. These are treated as separate identities with different profiles, security settings, and permissions. When they're asked to choose which account they want to use when they sign in, they should choose the identity that's a member in your directory. Only directory members can get access to your organization.

If you have a Visual Studio with MSDN subscription that [includes VSTS](https://visualstudio.microsoft.com/vs/pricing/), and you activated that subscription with a Microsoft account, you can add a work or school account. Azure AD manages that work or school account. Learn [how to link work or school accounts to Visual Studio with MSDN subscriptions](../../billing/link-msdn-subscription-to-organizational-account-vs.md).

<a name="faq-disconnect"></a>

## Disconnect from directory

### Why can't users sign in after my VSTS organization is disconnected?

They must now use Microsoft accounts to sign in. They can continue working seamlessly if they have Microsoft accounts with the same sign-in addresses that they use now.

If they must create Microsoft accounts with different sign-in addresses, you must add those addresses to your VSTS organization, and reassign access to them. They can migrate work that they want to keep, except work history. They might also have to re-link their MSDN
subscriptions. They can use any email address to create a Microsoft account.

<a name="get-support"></a>

[!INCLUDE [get-team-services-support](../../_shared/qa-get-vsts-support.md)]
