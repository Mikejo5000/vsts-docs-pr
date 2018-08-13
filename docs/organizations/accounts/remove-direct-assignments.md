---
title: Remove direct assignments
description: Learn how to remove direct assignments in your VSTS (Visual Studio Online, VSO, VSTS) organization
ms.prod: devops
ms.technology: devops-accounts
ms.topic: conceptual
ms.manager: douge
ms.author: chcomley
author: chcomley
ms.date: 04/20/2018
monikerRange: 'vsts'
---

# Remove direct assignments from users

[!INCLUDE [version-vsts-only](../../_shared/version-vsts-only.md)]

To manage a user's resources only by the groups that they're in, you must remove the direct assignments. Resources that are directly assigned to a user via individual assignment stay assigned to the user, whether the resources are assigned or taken away from the user's groups.

## Prerequisites

* You must be a member of the **Project Collection Administrators** group for the organization that you would like to manage users' direct assignments.

## Remove assignments

1. Sign in to your Visual Studio Team Services (VSTS) organization (`https://{yourorganization}.visualstudio.com`).

2. Under **Settings**, go to the **Users** tab.

3. Select all users with resources that should be managed only by groups.

4. From the command bar, select **Remove direct assignments**, or right-click and choose the same option from the menu.

   ![Choose remove direct assignments](_img/remove-direct-assignments/choose-remove-direct-assignments.png)

5. To confirm that you want to remove the direct assignments, select **Remove**.

Direct assignments are removed from the users.

> [!Note]
> If a user isn't a member of any groups, then the user isn't affected.

## Related articles

* [What is Azure Active Directory B2B Collaboration?](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)

* [Migrate to group-based resource management](migrate-to-group-based-resource-management-in-VSTS.md)

* [Assign access levels and extensions to users by group membership](assign-access-levels-and-extensions-by-group-membership.md)
