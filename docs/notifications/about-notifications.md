---
title: Understand the basics of how notifications work in VSTS and TFS
description: Understand how notifications or alerts are managed in Visual Studio Team Services (VSTS) or Team Foundation Server (TFS)
ms.prod: devops
ms.technology: devops-collab
toc: show
ms.manager: douge
ms.author: elbatk
author: elbatk
ms.topic: conceptual
ms.date: 09/01/2017
monikerRange: '>= tfs-2017'
---


# About notifications   

**VSTS | TFS 2018 | TFS 2017**

Notifications help you and your team stay informed about activity occuring within your Visual Studio Team Services (VSTS) or Team Foundation Server (TFS) team projects. With notifications, you are notified when changes occur to work items, code reviews, pull requests, source control files, and builds, you can be notified via email. For example, you can get notified whenever a bug that you opened is resolved or a work item is assigned to you. 

You receive notifications because of subscriptions. A subscription defines what types of notifications should be sent and the recipients of those notifications. There are differnt types of subscriptions: 

- **Built-in subscriptions**: useful "out of the box" subscriptions responsible for notifying about specific, common events like when a work item is assigned or a user is mentioned in pull request
- **Team subscriptions**: created by an admin to notify the team about events relevant to the team, like when a high priority bug is opened
- **Personal subscriptions**: created by a user to notify about activity the user cares about that is not cover d 

> [!NOTE]   
> Built-in subscriptions are also referred to as default subscriptions or out-of-the-box (OOB) subscriptions. These subscriptions cannot be modified or deleted.

You can manage your notifications, which you access from your account menu. Other notifications are managed by an administrator at these different levels: 

- Team subscriptions are managed by a team administrator
- Project subscriptions are managed by a member of the Project Administrators group, or delegate
- Account/collection subscriptions are managed by a member of the Project collection Administrators group, or delegate

## Preferred email address

Notifications are sent by default to the preferred email address for your account profile. This is typically the email address you signed into VSTS or TFS with, but can be managed via your account preferences profile page. 

> [!NOTE]   
> Your preferred email address applies across all of your accounts and cannot be changed on a per-account basis. 


## Integrating with other services 

If your team uses an external service to collaborate&mdash;such as Campfire, Flowdock, or Slack&mdash;you can configure notifications to be sent to these services. These services are supported out of the box:

- [Campfire](../service-hooks/services/campfire.md?toc=/vsts/notifications/toc.json&bc=/vsts/notifications/breadcrumb/toc.json) 
- [Flowdock](../service-hooks/services/flowdock.md?toc=/vsts/notifications/toc.json&bc=/vsts/notifications/breadcrumb/toc.json) 
- [Hipchat](../service-hooks/services/hipchat.md?toc=/vsts/notifications/toc.json&bc=/vsts/notifications/breadcrumb/toc.json) 
- [Slack](../service-hooks/services/slack.md?toc=/vsts/notifications/toc.json&bc=/vsts/notifications/breadcrumb/toc.json)  
- [Microsoft Teams](../service-hooks/services/teams.md?toc=/vsts/notifications/toc.json&bc=/vsts/notifications/breadcrumb/toc.json)

You can also use a third-party service like Zapier to send notifications to hundreds of other services. Learn more about [Zapier and VSTS integration](../service-hooks/services/zapier.md).

::: moniker range=">= tfs-2015 < vsts"

## On-premises SMTP server (TFS)
 
For on-premises TFS, [you must configure an SMTP sever](../tfs-server/admin/setup-customize-alerts.md) in order for team members to see the Notifications option from their account menu and to  receive notifications. 

::: moniker-end