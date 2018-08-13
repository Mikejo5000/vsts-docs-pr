---
title: Disconnect your VSTS organization from your Azure AD
description: Learn how to stop using your organization's directory and sign in with a Microsoft account by disconnecting your VSTS account from your directory
ms.prod: devops
ms.technology: devops-accounts
ms.assetid: 3eb744cf-854d-4cbd-b725-c2e070bd922b
ms.topic: conceptual
ms.manager: douge
ms.author: chcomley
author: chcomley
ms.date: 12/11/2017
monikerRange: 'vsts'
---
# Disconnect your VSTS organization from your directory

[!INCLUDE [version-vsts-only](../../_shared/version-vsts-only.md)]

<a name="DisconnectDirectory"></a>

To stop using your organization's directory and return to signing in with Microsoft accounts, you can disconnect your Visual Studio Team Services (VSTS) organization from your directory. 

For more information, see the [Conceptual overview](access-with-azure-ad.md) for using Azure Active Directory (Azure AD) with VSTS.

You need the following prerequisites:

*	[Microsoft accounts](`https://signup.live.com/`) for all users in your VSTS organization, including yourself as VSTS organization owner.

*	[VSTS organization ownership](faq-change-app-access.md#find-owner) for your Microsoft account. 

*	Global administrator permissions in your Azure AD for your Microsoft account as the VSTS organization owner. You need both because Azure AD users can't disconnect VSTS organizations from directories. You can add Microsoft accounts to a directory as external users. 

Learn about how to [Manage Azure administrators](https://azure.microsoft.com/documentation/articles/active-directory-assign-admin-roles/).

**What happens to current users?**  Users continue working seamlessly if they have Microsoft accounts that share the same sign-in addresses that they use now. Otherwise, users won't have access until you add them to VSTS as new users. Users can migrate everything except work history. They can relink Visual Studio subscriptions and have their access levels reassigned to their new identities.

0.	[Sign in to the Azure portal](https://portal.azure.com/) with your Microsoft account as the VSTS organization owner.

	[Why am I asked to choose between a work or school account and a personal account?](faq-azure-access.md#ChooseOrgAcctMSAcct)

0.	Browse to your VSTS organization. Select **All services**, and then enter **Team Services** in the **Filter** box. Choose **Team Services organizations**. If you recently browsed to **Team Services organizations**, you can select it from the recently accessed services on the left.

    ![Select Team Services organizations in the Azure portal](_img/manage-work-access/browse-to-team-services.png)

0. Select your organization.

    ![Select your organization in Azure portal](_img/manage-work-access/select-team-services-organization.png)

0.	Select **Disconnect**.

	![Configure the organization](_img/manage-work-access/azure-configure-disconnect.png)

0. Select **Yes** to confirm.

	![Disconnect the organization from directory](_img/manage-work-access/azuredisconnectdirectory1.png)

0.	Your VSTS organization is disconnected from your organization's directory.

	![Organization is now disconnected from your directory](_img/manage-work-access/azuredisconnectdirectory3.png)

	Only users with Microsoft accounts can sign in.
	
	> [!Important]
	> Before you disconnect your VSTS organization from your directory, make sure to **change the VSTS organization owner to a Microsoft account** and not to a school or work account. You can't sign in to your VSTS organization unless your work or school account has the same email address as your Microsoft account.

	For answers to questions about disconnecting, see the [FAQ](faq-azure-access.md#faq-disconnect).





