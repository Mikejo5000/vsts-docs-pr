---
ms.prod: vs-devops-alm
ms.technology: vs-devops-integrate
title: Notification event types | REST API Reference for Visual Studio Team Services and Team Foundation Server
description: REST APIs for Visual Studio Team Services and Team Foundation Server.
ms.assetid: 70F8A8F8-474C-4664-A26C-A5DC714E6242
ms.manager: douge
ms.author: elbatk
ms.date: 03/13/2017
---

# Notification event types
[!INCLUDE [API_version](../_data/version3-2-preview.md)]

[!INCLUDE [GET_STARTED](../_data/get-started.md)]

<a name="Get"></a>

## Get
Get a specific event type.


```no-highlight
GET https://{instance}/_apis/notification/eventtypes/{eventType}?api-version={version}
```


#### Authorization scopes
For more details, see section on how to [authorize access to REST APIs](../../get-started/auth/oauth.md).

| Scope | Name | Notes
|:------|:-----|:-----
| vso.notification | Notifications (read) | Provides read access to subscriptions and event metadata, including filterable field values.


#### Request parameters
| Name | In  | Type | Notes
|:--------------|:-----------|:---------|:------------
| <code>instance</code> | URL | string | Required. [VS Team Services account](/integrate/get-started/rest/basics.md#vs-team-services) ({account}.visualstudio.com) or [TFS server](/integrate/get-started/rest/basics.md#tfs) ({server:port}).
| <code>eventType</code> | URL | string | Required.
| <code>api-version</code> | Query | string | Required. [Version](../../get-started/rest/basics.md#versions) of the API to use.  This should be set to '3.2-preview' to use this version of the API.

#### Response

| Type       | Notes
|:-----------|:---------
| [NotificationEventType](./contracts.md#NotificationEventType) | Encapsulates the properties of an event type. It defines the fields, that can be used for filtering, for that event type.

[!code-REST [GET__notification_eventTypes__eventTypeId_.json](./_data/eventTypes/GET__notification_eventTypes__eventTypeId_.json)]

<a name="List"></a>

## List
List available event types for this service. Optionally filter by only event types for the specified publisher.


```no-highlight
GET https://{instance}/_apis/notification/eventtypes?api-version={version}
```


#### Authorization scopes
For more details, see section on how to [authorize access to REST APIs](../../get-started/auth/oauth.md).

| Scope | Name | Notes
|:------|:-----|:-----
| vso.notification | Notifications (read) | Provides read access to subscriptions and event metadata, including filterable field values.


#### Request parameters
| Name | In  | Type | Notes
|:--------------|:-----------|:---------|:------------
| <code>instance</code> | URL | string | Required. [VS Team Services account](/integrate/get-started/rest/basics.md#vs-team-services) ({account}.visualstudio.com) or [TFS server](/integrate/get-started/rest/basics.md#tfs) ({server:port}).
| <code>api-version</code> | Query | string | Required. [Version](../../get-started/rest/basics.md#versions) of the API to use.  This should be set to '3.2-preview' to use this version of the API.
| <code>publisherId</code> | Query | string | Optional. Limit to event types for this publisher

#### Response

| Type       | Notes
|:-----------|:---------
| VssJsonCollectionWrapper&lt;array ([NotificationEventType](./contracts.md#NotificationEventType))&gt; |

### All
[!code-REST [GET__notification_eventTypes.json](./_data/eventTypes/GET__notification_eventTypes.json)]

### By publisher
[!code-REST [GET__notification_eventTypes_publisherId-_publisherId_.json](./_data/eventTypes/GET__notification_eventTypes_publisherId-_publisherId_.json)]