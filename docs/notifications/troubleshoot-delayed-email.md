---
title: Why are my notification emails delayed
titleSuffix: VSTS & TFS 
description: Troubleshooting steps for delayed emails from notifications in Visual Studio Team Services (VSTS) and Team Foundation Server (TFS)
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

<b>VSTS | TFS 2018 | TFS 2017.1 | [Previous versions](../work/track/alerts-and-notifications.md)</b> 

> [!NOTE]  
> This topic applies to VSTS, TFS 2017 Update 1, and later versions. If you work from an on-premises TFS 2017 or ealier versions, see [Set alerts, get notified when changes occur](../work/track/alerts-and-notifications.md). For on-premises TFS, [you must configure an SMTP server](/tfs/server/admin/setup-customize-alerts) in order for team members to see the Notifications option from their organization menu and to receive notifications.

# Emails from VSTS subscriptions or notifications are delayed
An email is generated when an [event](oob-supported-event-types.md) occurs within VSTS which matches a notification subscription. See the [notifications overview](about-notifications.md) for more information about notification subscriptions.

If you're not receiving an expected notification email, it could be for the following reason:
* Your organization is creating a very large volume notifications

Please perform the following step to determine if it resolves the issue.

## Step 1: Check the notification statistics for unexpectedly high volume
Poorly defined subscription filters or duplicate subscriptions might cause an unexpected high volume of notifications, causing a delay in the processing or delivery of emails.  Click [here](howto-view-organization-notification-statistics.md) to learn how to view and analyze notification statistics.

## Contact customer support
If you're not able to resolve the issue with the steps above, consider contacting [customer support](troubleshoot-contact-support.md)