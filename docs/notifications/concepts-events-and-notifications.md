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
Events are raised in the system when changes occur within the system.  Actions like creating or updating a work item will cause an event to be raised.  The list of supported event types can be found [here](oob-supported-event-types.md).

## Subscriptions
A notification subscription is associated with a [supported event type](oob-supported-event-types.md) and includes a set of filters which are used to match events with the subscription. For example, a subscription for a work item created event might include a filter which matches only the work item type `Bug`, or a subscription for a pull request created event might include a filter for a specific `Repositiry and branch`.

TODO:  this should probably mention event vs. delivery properties of the subscription.

### Default email subscriptions
Many useful email subscriptions are pre-defined and enabled by default in the system. These are considered `Default subscriptions`.  The list of default subscription can be found [here](oob-build-in-notifications.md).

An account or team adminstrator can choose which of the pre-defined subscriptions to make available to their users.  Also, users can choose to opt-out of any default subscription while other team members continue to be be subscribed.

### Custom email subscriptions


### Custom service hook subscriptions

## Notifications
When an event is raised in the system, it is compared with every subscription of the specified event type.  The event content is matched against the filter conditions defined in the subscription. A notifications is generated when a subscription's filter conditions match the event conent.  A separate notification is generated for each subscription/event match.

Each notification is then delivered either as an email or as a service hook based on delivery properties defined in the subsription.
