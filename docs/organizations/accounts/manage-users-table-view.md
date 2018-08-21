---
title: Manage users and access in Azure DevOps Services
description: Add users and assign access levels on the Users page in Azure DevOps Services. 
ms.prod: devops
ms.technology: devops-accounts
ms.assetid: 9f142821-1772-413f-a0e0-9b47b11a410f
ms.topic: conceptual
ms.manager: douge
ms.author: chcomley
author: chcomley
ms.date: 07/31/2018
monikerRange: 'vsts'
---
# Manage users for Azure DevOps Services

[!INCLUDE [version-vsts-only](../../_shared/version-vsts-only.md)]

Learn how to add users to your Azure DevOps Services organization and specify the level of features they can use, such as Basic or Stakeholder.

These types of users can join your Azure DevOps Services organization for free:

*	Five users who get [Basic features](https://visualstudio.microsoft.com/team-services/compare-features/), such as version control and tools for Agile, Java, and build and release management.
*	Unlimited users who get [Stakeholder features](https://visualstudio.microsoft.com/team-services/compare-features/), such as working with your backlog, work items, and queries.
*	Unlimited [Visual Studio subscribers](https://visualstudio.microsoft.com/team-services/compare-features/) who also get Basic features. In some cases, these users get additional features with specific extensions, such as [Test Manager](https://marketplace.visualstudio.com/items?itemName=ms.vss-testmanager-web). 

Need [more users with Basic features or Visual Studio subscriptions](../billing/buy-basic-access-add-users.md)?

> [!NOTE]
> You can add people to projects instead of to your organization. Azure DevOps Services automatically assigns the users [Basic features](https://visualstudio.microsoft.com/team-services/compare-features/) if your organization has seats available, or [Stakeholder features](https://visualstudio.microsoft.com/team-services/compare-features/) if not. Learn [how to add members to projects](add-team-members-vs.md).
>
> When people don't need access to your Azure DevOps Services organization anymore, [delete them](delete-organization-users.md) from your organization. 

## Prerequisites

You must have [Azure DevOps Services project collection administrator or organization owner permissions](../../organizations/security/set-project-collection-level-permissions.md?toc=/vsts/organizations/accounts/toc.json&bc=/vsts/organizations/accounts/breadcrumb/toc.json).   


##	Manage users

The Users view shows key information per user in a table. In this view, you can:
* See and modify assigned service extensions and access levels.
* Multi-select users and bulk edit their extensions and access.
* Filter by searching for partial user names, access level, or extension names.
* See the last access date for each user. This can help you choose users to remove access from or lower access to stay within your license limits.

[!INCLUDE [temp](../../boards/_shared/new-agile-hubs-feature.md)]

# [New navigation](#tab/new-nav)

1. Sign in to your Azure DevOps Services organization (```https://dev.azure.com/{yourorganization}```).

	[Why am I asked to choose between my work or school account and my personal account?](faq-create-organization.md#ChooseOrgAcctMSAcct)

2. Go to your Azure DevOps Services admin settings.

    ![Open Azure DevOps Services admin settings](../../_shared/_img/settings/open-admin-settings-vert.png)

3. Select the **Users** tab, and then select **Add new users**.

   ![Select the Users tab, and then select Add new users](_img/_shared/add-new-users.png)

4. Select a user or group of users. Then, select the **...** icon at the end of the **Name** column to open the context menu. 

    In the context menu, select one of these options:
    *   **Add to projects**
    *   **Remove from projects**
    *   **Assign extensions**
    *   **Revoke extensions** (if there are extensions)
    *   **Change access levels**
    *   **Remove direct assignments**
    *   **Remove from organization** (deletes user)

    ![Select the Users hub, and then select an item in the context menu](_img/manage-users/manage-users-show-context-menu-vert.png)

5. **Save** your changes.

# [Previous navigation](#tab/prev-nav)
 
1. Open the **Users** page for your organization. Select the ![gear icon](../../_img/icons/gear-icon.png) **Settings** icon, and then select **Organization Settings**.
 
	![Open Organization Settings](../../_shared/_img/settings/open-organization-settings.png)

	Select **Users** to open the **Manage users** page. Then, select **Add new users**. 

	![Open the Add new users page](../../user-guide/_img/sign-up/add-new-users.png)

2. Select a user or group of users. Then, select the **...** icon at the end of the **Name** column to open the context menu. 

    In the context menu, select one of these options:
    *   **Change access levels**
    *   **Manage projects**
    *   **Resend invite**
    *   **Manage extensions** (if there are extensions)
    *   **Remove from organization** (deletes user)

   ![Select the User hub, and then select an item in the context menu](_img/manage-users/manage-users-show-context-menu.png)


### How is *access* different from *permissions*?

Access levels control which features are available to users. Permissions control a user's access to organization resources. To learn more, see [Default permissions and access](../../organizations/security/permissions-access.md). 

## Related articles

- [Change number of paid extension users](../billing/change-number-paid-extension-users.md)
- [Connect to a project](../../organizations/projects/connect-to-projects.md)
- [Change individual permissions or grant select access to specific functions](../../organizations/security/change-individual-permissions.md)
- [Grant or restrict access to select features and functions](../../organizations/security/restrict-access.md)
- [Delete users from Azure DevOps Services](delete-organization-users.md)

