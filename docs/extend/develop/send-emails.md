---
ms.prod: vs-devops-alm
ms.technology: vs-devops-extensions-api
title: Send Email Notifications | Extensions for VSTS
description: Send email notifications from your VSTS extensions.
ms.assetid: A144FA80-8509-4E22-9D87-D14FCA4481E5
ms.manager: douge
ms.author: wismythe
ms.date: 06/14/2018
---

# Send email notifications from VSTS extensions

Notifications are an important way to keep users of your extension informed about activity by other users. For example, an extension that manages shared notes for a team can notify the team when a new note is created or can notify the creator of a note when someone else comments on it. 

## Registering an event type

All notifications originate from an event published into the VSTS notifications pipeline. Events are typically triggered when a user performs some activity like updating a work item or installing an extension.  Events published into the pipeline must indicate their type, and this type must be known to VSTS. Events of the same type have the same structure and are typically rendered by the same email template.

Event types are registered as contributions of type `ms.vss-notifications.event-type` that targets the `ms.vss-extmgmt-web.extensions-event-publisher` event publisher. 

 ### Example

```json
{
    "contributions": [
        {
            "id": "note-event",
            "type": "ms.vss-notifications.event-type",
            "targets": [
                "ms.vss-extmgmt-web.extensions-event-publisher",
                "ms.vss-extmgmt-web.extensions-event-category"
            ],
            "properties": {
                "name": "Note event",
                "description": "Event that represents when a note is added, updated, or deleted.",
                "customSubscriptionsAllowed": false,
                "hasInitiator": true,
                "icon": "bowtie-packages",
                "supportedScopes": [
                    "project",
                    "collection"
                ],
                "roles": [
                    {
                        "id": "initiator",
                        "name": "Initiator"
                    },
                    {
                        "id": "team",
                        "name": "Team"
                    },
                    {
                        "id": "creator",
                        "name": "Creator"
                    }
                ]
            }
        }
    ]
}
```

* `id` should describes the activity that triggers events of this type

* `roles` should describes the potential roles of actors (users or groups) on published events of this type. Roles make it easier for users to create custom subscriptions that control who (what roles) gets notified about a particular event. In this example, there are 3 roles associated with a note event: the user that made the change (the initiator of the event), the team associated with the team, and the creator of the note (which will be the same as the initiator when the note is first created).

## Registering a default subscription

Default subscriptions are built-in notification rules that appear in the user's personal notification settings page and result in users getting notified about specific activity relevant to them. These subscriptions are automatically enabled by default, but users can turn them off. Learn more about [default subscriptions](../../notifications/manage-personal-notifications.md).

Register one or more default subscriptions as contributions in your extension manifest. Each subscription provides a description to help users understand what the subscription does and indicates who (which actors, based on role) should be notified for a particular event.

### Example

```json
{
    "contributions": [
        {
            "id": "note-event-subscription",
            "type": "ms.vss-notifications.subscription",
            "targets": [
                "ms.vss-notifications.default-subscription-collection"
            ],
            "properties": {
                "description": "A note was added, changed, or deleted",
                "filter": {
                    "type": "Actor",
                    "eventType": "my-publisher.my-extension.note-event",
                    "inclusions": [
                        "team",
                        "creator"
                    ],
                    "exclusions": [
                        "initiator"
                    ],
                    "criteria": {}
                }
            }
        }
    ]
}
```

* `id` should describe the subscription. In simple cases, this value will be similar to the ID of the associated event type contribution. In more complex cases, this ID should further clarify what makes it unique compared to other subscriptions for the same event type.
* `targets` must always include `ms.vss-notifications.default-subscription-collection`
* `filter` indicates the rules that get evaluated when an event of the specified event type is published. In this example, the rules are simple: when a note is created, added, or deleted, send a notification to the creator of the note and all team members, but don't sent a notification to the user that made the change.
* `eventType` indicates the fully-qualified ID of the event type this subscription is associated with. In this example, both the event type and the default subscription contribution are defined in the same extension, which has an ID of `my-publisher.my-extension`.

## Registering an email template

If a published event matches the filter rules of your default subscription, one or more notifications will be produced based on the included actors defined by the subscription. An email template is then applied to produce the actual email that gets sent to the intended recipients.

Just like event types and default subscriptions, email templates are defined by contributions. A simple email with basic heading, call to action, and footer can be created with a simple.

### Example

```json
{
    "contributions": [
        {
            "id": "note-event-email-template",
            "type": "ms.vss-notifications.email-template",
            "targets": [
                ".note-event"
            ],
            "includes": [
                "ms.vss-notifications.standard-email-template"
            ],
            "properties": {
                "sourceTemplate": "ms.vss-notifications.standard-email-template",
                "inputs": {
                    "email-subject": "[{{ event.team.name }}] Note {{{ event.action }}} by {{ event.user.name }}",
                    "summary": "{{ event.user.name }} {{ event.action }} note {{ event.note.title }}",
                    "hero": {
                        "title": "Note {{{ event.action }}} in {{ event.team.name }}",
                        "message": "{{ event.note.title }}",
                        "action": {
                            "title": "Open notes",
                            "url": "{{{ event.links.web }}}"
                        }
                    }
                }
            }
        }
    ]
}
```

## Publishing events

To publish an event from your extension, you first need to ensure your extension manifest lists the necessary scope:

```json
{
    "scopes": [
        "vso.notification_publish"
    ]
}
```

> If you previously published your extension without this scope and it has already been installed, an admin in the account will need to authorize this new scope before your extension gets upgraded in the account.

To publish an event from the client extension, use the platform-provided client service and publish a `VssNotificationEvent`. Here is an example:

```javascript

import VSS_Common_Contracts = require("VSS/WebApi/Contracts");
import Notifications_Extensions = require("Notifications/Extensions");

export function publishEvent(eventData: any) {

    const notificationEvent: VSS_Common_Contracts.VssNotificationEvent = {
        eventType: VSS.getExtensionContext().publisherId + "." + VSS.getExtensionContext().extensionId + "." + "note-event",
        actors: [
            {
                id: eventData.user.id,
                role: "initiator"
            },
            {
                id: eventData.team.id,
                role: "team"
            },
            {
                id: eventData.creator.id,
                role: "creator"
            }
        ], 
        data: data,
        artifactUris: [],
        scopes: <VSS_Common_Contracts.EventScope[]>[
            {
                id: VSS.getWebContext().collection.id,
                type: "collection"
            },
            {
                id: VSS.getWebContext().project.id,
                type: "project"
            }
        ]
    };

    Notifications_Extensions.publishEvent(notificationEvent);
}
```

Your web extension can then call `publishEvent` with the appropriate data. For example:

```javascript
import Locations = require("VSS/Locations");


var eventData =  {
    action: "created",
    note: note,
    user: VSS.getWebContext().user,
    team: VSS.getWebContext().user,
    creator: VSS.getWebContext().user,
    links: {
        web: Locations.urlHelper.getMvcUrl({ 
                controller: "apps",
                action: "hub",
                parameters: [ VSS.getContribution().id ] })
    }
};

publishEvent(eventData);
```


