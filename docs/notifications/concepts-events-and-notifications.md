---
title: Events, subscriptions, and notifications
titleSuffix: VSTS & TFS 
description: Events, subscriptions, and notifications
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


# Events, subscriptions, and notifications

<b>VSTS | TFS 2018 | TFS 2017.1 | [Previous versions](../work/track/alerts-and-notifications.md)</b> 

> [!NOTE]  
> This topic applies to VSTS and to TFS 2017.1 and later versions. If you work from an on-premises TFS 2017 or ealier versions, see [Set alerts, get notified when changes occur](../work/track/alerts-and-notifications.md). For on-premises TFS, [you must configure an SMTP server](/tfs/server/admin/setup-customize-alerts) in order for team members to see the Notifications option from their account menu and to receive notifications.

## Events
Events are raised in VSTS when changes occur within the system.  Actions like creating or updating a work item will cause an event to be raised.  The list of supported event types can be found [here](oob-supported-event-types.md).

## Subscriptions
A notification subscription is associated with a [supported event type](oob-supported-event-types.md) and includes a set of filters which are used to match events with the subscription. For example, a subscription for a work item created event might include a filter which matches only the work item type `Bug`, or a subscription for a pull request created event might include a filter for a specific `Repositiry and branch`.

### Default email subscriptions
Many useful email subscriptions are pre-defined and enabled by default in the system. These are considered `Default subscriptions`.  Default subscriptions are intended to provide the out of box support for the most common notification scenarios.  The list of default subscription can be found [here](oob-built-in-notifications.md).

An account or team adminstrator can choose which of the default subscriptions to make available to their users.  Click [here](howto-manage-team-notifications.md) to learn how to manage team notifications, or [here](howto-manage-account-notifications.md) to learn how to manage account level notifications.

Users can choose to opt-out of any default subscription while other team members continue to be be subscribed.  Click [here](howto-manage-personal-notifications.md) to learn more about managing personal subscriptions.

### Custom email subscriptions
Custom email subscriptions can be created by account or team administrators which appy to all members of the account or team.  Click [here](howto-manage-team-notifications.md) to learn how to manage team notifications, or [here](howto-manage-account-notifications.md) to learn how to manage account level notifications.

Individuals can also create custom subscriptions which apply only to them. Click [here](howto-manage-personal-notifications.md) to learn more about managing personal subscriptions.

### Custom service hook subscriptions
Service hooks subscriptions are used to integrate with third party services.  When a VSTS event matches a service hook subscription, a notification is delivered to the third part service.  For example, when a VSTS build completes a notification can be delivered to a Slack channel with links back to the build artifact in VSTS.  To learn more see [Integrating with Third Party Services](howto-integrate-third-party-services.md)

## Notifications
When an event is raised in the system, it is compared with every subscription of that event type.  The event content is matched against the subscripition's filter conditions. If the filter conditions are met, a notifications is generated.  A notification is generated for every subscription/event match.

Each notification is then delivered either as an email or as a service hook based on delivery properties defined in the subsription.  Click [here](concepts-email-delivery-options.md) to learn more about email delivery options.
