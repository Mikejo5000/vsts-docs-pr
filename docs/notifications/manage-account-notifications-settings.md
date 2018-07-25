---
title: Manage notifications for a team
titleSuffix: VSTS & TFS 
description: Manage account notification settings
ms.technology: devops-collab
ms.prod: devops
ms.assetid: 6edc44d0-2729-46f5-8108-c8a5160a6a7a
ms.manager: douge
ms.reviewer: wismythe
ms.author: elbatk
author: elbatk
ms.topic: conceptual
ms.date: 07/25/2018
monikerRange: '>= tfs-2017'
---

# Manage account notification settings

<b>VSTS | TFS 2018 | TFS 2017.1 | [Previous versions](../work/track/alerts-and-notifications.md)</b> 

> [!NOTE]  
> This topic applies to VSTS and to TFS 2017.1 and later versions. If you work from an on-premises TFS 2017 or ealier versions, see [Set alerts, get notified when changes occur](../work/track/alerts-and-notifications.md). For on-premises TFS, [you must configure an SMTP server](/tfs/server/admin/setup-customize-alerts) in order for team members to see the Notifications option from their account menu and to receive notifications. 

Account level notification settings can be used to set defaults which apply to all groups unless explictily overriden.

## How to navigate to account level notification settings

The direct URL is `https://{account}.visualstudio.com/_admin/_notifications?view=settings`.  Or follow these steps to navigate through the UI.

1. Open the Notifications hub under account settings

    ![Account notifications under settings menu](_img/manage-account-notifications-settings-menu.png)

2. Click **Settings**.

    ![Account notifications settings tab](_img/manage-account-notifications-settings-tab.png)

## Manage the account level notification delivery setting
The account level notification delivery setting defines the default setting for all groups in this account.  This option is inherited by every group and will apply to a group's notification subscriptions unless explicitly overriden by that group's delivery setting.

1. Choose to allow or block delivery of emails to group members.

    ![Account notification settings delivery option](_img/manage-account-notifications-settings-delivery.png)