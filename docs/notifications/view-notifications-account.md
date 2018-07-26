---
title: Manage notifications for a team
titleSuffix: VSTS & TFS 
description: Get notified when changes occur to source code, git, work items, and builds in Visual Studio Team Services & Team Foundation Server  
ms.technology: devops-collab
ms.prod: devops
ms.assetid: 6edc44d0-2729-46f5-8108-c8a5160a6a7a
ms.manager: douge
ms.reviewer: wismythe
ms.author: elbatk
author: elbatk
ms.topic: conceptual
ms.date: 12/14/2017  
monikerRange: '>= tfs-2017'
---


# View notifications for an account

<b>VSTS | TFS 2018 | TFS 2017.1 | [Previous versions](../work/track/alerts-and-notifications.md)</b> 

> [!NOTE]  
> This topic applies to VSTS and to TFS 2017.1 and later versions. If you work from an on-premises TFS 2017 or ealier versions, see [Set alerts, get notified when changes occur](../work/track/alerts-and-notifications.md). For on-premises TFS, [you must configure an SMTP server](/tfs/server/admin/setup-customize-alerts) in order for team members to see the Notifications option from their account menu and to receive notifications.

## Account level notification hub URL
```
https://{account}.visualstudio.com/_admin/_notifications
```

## Navigating to the account level notification hub
Choose the Notifications hub under account settings.

![Navigate to account notifications hub](_img/nav-account-notifications-hub.png)

## The account notification hub

The account notification hub consists of the following sections
* Default subscritions - view all [default notification subscriptions](./oob-built-in-notifications.md)
* Subscribers - view notification subscriptions for a specific group, team, or individual
* Statistics - view the most active subscriptions and top event initiators
* Settings - manage account level settings such as delivery perferences

![View account level notification hub](_img/view-account-notification-hub.png)

## Account notification hub: Default subscriptions

The `Default subscriptions` section lists all default subscriptions available to the account. The globe icon on a notification subscription indicates the subscription is a default subscription.

Members of the project collection administrators group have permission to enable/disable any default subscription in this view.  Any member project collection valid users have permission to view the details of the default subscription.  The view and enablement options are available in the context menu (`...`) associated with each individual subscription.

![Account level notification hub: Default subscriptions](_img/view-account-notification-default-subscriptions.png)

## Account notification hub: Subscribers

The `Subscribers` section begins with empty identity search box. Enter any group, team, or individual to view the list of subscriptions associated with the specified identity.

![Account level notification hub: Subscribers empty](_img/view-account-notification-subscribers-empty.png)

All notification subscription associated with the specified identity are listed in this view which include [default subscriptions]() and [custom subscriptions]().  Subscribers have options to [add](), [remove](), [edit](), or [toggle the enablement]() of a customer subscription.  Subscribers can also [opt-in or opt-out]() of a default subscription in this view.  Management options are available from the context menu (`...`) associated with each subscription.

Note, the globe icon on subscription row indicates a default subscription while custom subscriptions have no assiciated icon.

![Account level notification hub: Subscribers list](_img/view-account-notification-subscribers.png)

