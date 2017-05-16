---
title: Library for Visual Studio Team Services and Team Foundation Server
description: Understand the library in Microsoft Release Management for Visual Studio Team Services (VSTS) and Team Foundation Server (TFS)
ms.assetid: 45C5042C-9E31-41F8-B63B-6D5C241EEC21
ms.prod: vs-devops-alm
ms.technology: vs-devops-release
ms.topic: get-started-article
ms.manager: douge
ms.author: ahomer
ms.date: 10/20/2016
---

# Library

**TFS 2017 | Team Services**

*Library* is a collection of _shared_ build and release assets for a team project.
Assets defined in a library can be used in multiple build and release definitions of the team project.
The **Library** tab can be accessed directly in the **Build &amp; Release** hub in Team Services and Team Foundation Server.

At present, the library contains only one type of asset: [variable groups](variable-groups.md).
The following types of assets are not yet present in the **Library** tab, but soon will be:

* [Task groups](task-groups.md)
* [Service endpoints](service-endpoints.md)

Although these assets are not present in the **Library** tab,
they are still shared across build and release definitions in a team project.

> Variable groups are available to only release definitions in Team Services and TFS 2017 at present.
Task groups and service endpoints are available to build and release definitions in TFS 2015, TFS 2017, and Team Services.

<h2 id="security">Library Security</h2>

All assets defined in the **Library** tab share a common security model. You can control who can define new items in a library,
and who can use an existing item. **Roles** are defined for library items, and **membership** of these roles governs the
operations you can perform on those items.

| Role on a library item | Purpose |
|-------------------------|---------|
| Reader | Members of this role can view the item. |
| User | Members of this role can use the item when authoring build or release definitions. For example, you must be a 'User' for a variable group to be able to use it in a release definition.  |
| Administrator | In addition to all the above operations, members of this role can manage membership of all other roles for the item. The user that created an item is automatically added to the Administrator role for that item.

The security settings for the **Library** tab control access for _all_ items in the library. Role memberships for individual items are automatically inherited from those of the **Library** node.
In addition to the three roles listed above, the **Creator** role on the library defines who can create new items in the library, but cannot be used to manage permissions for other users.
By default, the following groups are added to the **Administrator** role of the library: **Build Administrators**, **Release Administrators**, and **Project Administrators**.

[!INCLUDE [rm-help-support-shared](../../_shared/rm-help-support-shared.md)]
