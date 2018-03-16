---
title: Differences and limitations for non-members
titleSuffix: Azure CodeX Public Project
description: Differences and limitations for non-members
ms.prod: vs-devops-alm
ms.technology: vs-devops-admin
ms.assetid: 
toc: show
ms.manager: douge
ms.author: kaelli
ms.topic: get-started-article
ms.date: 02/20/2018
---


# Differences and limitations for non-members of a public project

**Azure CodeX Public Project**

In a public project, most CodeX features work the same for members and non-members.
Non-members get read-only access to the project, and members have the access their permissions specify.
There are some features which work differently or are completely unavailable for non-members.
Over time, we intend to reduce the number of differences and increase the availability of other features.

## Differences between a public and private project
When marking a project public, there are two changes which affect all members of the project:
* Permissions marked "deny" are not honored. The permissions automatically granted to a non-member act as a "floor" on the capabilities that can be assigned to any member in the project.
* If a build definition specifies Project Collection scope, it will run with Project scope instead. This reduces the risk if a malicious user exfiltrates the build service's authentication token.

## Features unavailable for non-members

* Any form of editing or creating artifacts
* Favoriting and following existing artifacts
* Settings & administration
* Team Foundation Version Control (TFVC)
* XAML build system
* Manual and Cloud Load Testing
* Package Management
* Paid extensions

## Features with differences for non-members

### Identity and user information
Information about members of the project is limited to their name and picture.
Email addresses and other contact information are not available.
Also, lists of artifacts cannot be filtered by identity.

### Navigation
Non-members cannot switch between two public projects in the same account, even though they can navigate there directly using a URL.

### Work item tracking
The work item tracking area is limited to work items.
Backlogs, boards, sprints, queries, and plans are not available.

### Version control
Git repositories can be browsed and cloned, but only via HTTPS.
SSH and GVFS endpoints are unavailable.
Clients like Visual Studio and IntelliJ work with the HTTPS clone URL but don't offer the connected experience linking to work items and other collateral.

### CI/CD
The definition & task editors are not available to non-members.
The environment summary page and library views are not available.
Only the new Release views are available, so there is no fallback to the old views when functionality hasn't yet been added in the new ones.

### Analytics & dashboards
The analytics OData feed, cross-project queries, and analytics views are not available.

The following Dashboard widgets are not available:

* Assigned to me
* Code tile
* New work item
* Pull request
* Query results
* Requirements quality
* Sprint burndown
* Sprint capacity
* Sprint overview
* Team members
* Welcome
* Work links
* Other links
