---
title: Manage notifications for an organization
titleSuffix: VSTS & TFS 
description: Manage notifications for an organization in Visual Studio Team Services (VSTS) or Team Foundation Server (TFS)
ms.technology: devops-collab
ms.prod: devops
ms.manager: douge
ms.reviewer: wismythe
ms.author: elbatk
author: elbatk
ms.topic: conceptual
ms.date: 08/06/2018
monikerRange: '>= tfs-2017'
---


# Manage notifications for an organization

<b>VSTS | TFS 2018 | TFS 2017.1 | [Previous versions](../work/track/alerts-and-notifications.md)</b> 

> [!NOTE] 
> This topic applies to VSTS, TFS 2017 Update 1, and later versions. If you work from an on-premises TFS 2017 or ealier versions, see [Set alerts, get notified when changes occur](../work/track/alerts-and-notifications.md). For on-premises TFS, [you must configure an SMTP server](/tfs/server/admin/setup-customize-alerts) in order for team members to see the Notifications option from their organization menu and to receive notifications.

## Organization level notifications hub
See [Navigating the UX](navigating-the-ux.md) to learn how to locate this hub.

The organization notifications hub consists of the following sections:
* Default subscriptions - view all [default notification subscriptions](./oob-built-in-notifications.md)
* Subscribers - view notification subscriptions for a specific group, team, or individual
* Statistics - view the most active subscriptions and top event initiators
* Settings - manage organization level settings such as delivery preferences

## Organization notifications hub: Default subscriptions

The `Default subscriptions` section lists all default subscriptions available to the organization. The globe icon on a notification subscription indicates the subscription is a default subscription.

Members of the **project collection administrators** group have permission to enable/disable any default subscription in this view. Any member project collection valid users have permission to view the details of the default subscription. The view and enablement options are available in the context menu (`...`) associated with each individual subscription.

![Organization level notifications hub: Default subscriptions](_img/view-organization-notification-default-subscriptions.png)

## Organization notifications hub: Subscribers

The `Subscribers` section begins with an empty identity search box. Enter any group, team, or individual to view the list of subscriptions associated with the specified identity.

![Organization level notifications hub: Subscribers empty](_img/view-organization-notification-subscribers-empty.png)

All notification subscriptions for the chosen identity are listed in this view. Management options are available from the context menu (`...`) associated with each subscription. Note, the ![globe](_img/oob-notification.png) icon on subscription row indicates a default subscription.

![Organization level notifications hub: Subscribers list](_img/view-organization-notification-subscribers.png)

## Organization notifications hub: Statistics

The `Statistics` section shows the most active notification subscriptions and the top event initiators (group, team, or individual). The statistics are only for the current day and reset at 00:00 UTC. A benefit of these statistics is identifying unintended high volume subscriptions or event initiators.

![Organization level notifications hub: Statistics](_img/view-organization-notification-stats.png)

## Organization notifications hub: Settings

The `Settings` section allows organization level notification settings to be managed by any member of the **project collection administrators** group. The _Default delivery option_ setting is inherited by all teams and groups, and therefore is not explicitly set at the team or group level.

![Organization level notifications hub: Settings](_img/view-organization-notification-settings.png)