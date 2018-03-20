---
title: Inviting outside users
titleSuffix: Azure CodeX Public Project
description: Security and data access considerations when adding a member
ms.prod: vs-devops-alm
ms.technology: vs-devops-admin
ms.assetid: 
toc: show
ms.manager: douge
ms.author: kaelli
ms.topic: get-started-article
ms.date: 02/20/2018
---

# Inviting outside users

**Azure CodeX Public Project**

The team project is a container and security boundary for your software development assets: work items, code, builds, etc.
A non-member can access only the contents of a public project and nothing else in your account.
A project member, on the other hand, has access to account-level resources and additional groups (or scopes) beyond the project.
When you add someone as a member of a public project, you are also trusting that person with these additional privileges.

## Additional groups & scopes

Under the hood, a project member belongs to one or more [project-related VSTS groups](../security/about-security-identity.md#security-groups-and-permissions) such as "Project Valid Users" and "Project Contributors".
That person is also a member of an account-level group known as "Project Collection Valid Users".
Also, that person's identity appears in the [identity service](../security/about-security-identity.md#authentication) which backs the account.
In VSTS accounts backed by [Azure Active Directory](/azure/active-directory/), identities may be [native](/azure/active-directory/add-users-azure-active-directory) or [guests](/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b), which grant different levels of access.

## Account-level resources

Project members have access to resources beyond the specific project.
Those resources are:

* All [VSTS features](feature-differences.md), such as TFVC, Agile boards & backlogs, and WIT queries
* Information about other members, including their email address and other contact details, that is hidden from non-members
* All installed extensions, including paid extensions (if you assign a license)
* [Process model](../work/customize/process/manage-process.md) metadata, such as the valid values of all picklists in the account
* The settings area, including the list of users
* Higher [rate limits](../collaborate/rate-limits.md) than an anonymous user

## Making a trust decision

These resources and groups are required for the proper functioning of a member of a project.
Public projects don't fundamentally change the level of trust that you make when you decide to add someone to a project in VSTS.
However, in a private project, your collaborators are typically colleagues and others whom you have an existing relationship with.
Hosting a public project may invite attention from people across the world and that you've never met before.
Before you add someone to a project, think first whether they should have access to the items mentioned above.
