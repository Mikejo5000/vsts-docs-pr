---
title: Azure function task for Microsoft VSTS and TFS 
description: Build and release task to invoke a HTTP triggered function in an Azure function app and parse the response in VSTS and TFS
ms.assetid: 8D3F3DAA-92C8-4631-96C6-938D43C60008
ms.prod: devops
ms.technology: devops-cicd
ms.topic: reference
ms.manager: douge
ms.author: ahomer
author: alexhomer1
ms.date: 04/09/2018
monikerRange: '>= tfs-2017'
---

# Utility: Invoke Azure function

**VSTS**

![icon](_img/azure-function.png) &nbsp; Invoke a HTTP triggered function in an Azure function app and parse the response.

## Demands

Can be used in only an [agentless phase](../../concepts/process/server-phases.md) of a release definition.

## Arguments

| Parameter | Comments |
| --- | --- |
| **Azure function URL** | Required. The URL of the Azure function to be invoked. |
| **Function key** | Required. The value of the available function or the host key for the function to be invoked. Should be secured by using a hidden variable. |
| **Method** | Required. The HTTP method with which the function will be invoked. |
| **Headers** | Optional. The header in JSON format to be attached to the request sent to the function. |
| **Query parameters** | Optional. Query parameters to append to the function URL. Must not start with "**?**" or "**&**". |
| **Body** | Optional. The request body for the Azure function call in JSON format. |
| **Completion Event** | Required. How the task reports completion. Can be **API response** (the default) - completion is when function returns success and success criteria evaluates to true, or **Callback** - the Azure function makes a callback to update the timeline record. |
| **Success criteria** | Optional. How to parse the response body for success. |
| **Control options** | See [Control options](../../concepts/process/tasks.md#controloptions) |

Succeeds if the function returns success and the response body parsing is successful, or when the function updates the timeline record with success.

For more information about using this task, see [Approvals and gates overview](../../concepts/definitions/release/approvals/index.md).

Also see this task on [GitHub](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/AzureFunction).

::: moniker range="vsts"

## YAML snippet

```YAML
- task: AzureFunction@1
  inputs:
    function: 
    key: 
    #method: 'POST' # Options: oPTIONS, gET, hEAD, pOST, pUT, dELETE, tRACE, pATCH
    #headers: '{Content-Type:application/json, PlanUrl: $(system.CollectionUri), ProjectId: $(system.TeamProjectId), HubName: $(system.HostType), PlanId: $(system.PlanId), JobId: $(system.JobId), TimelineId: $(system.TimelineId), TaskInstanceId: $(system.TaskInstanceId), AuthToken: $(system.AccessToken)}' 
    #queryParameters: # Optional
    #body: # Required when method != GET && Method != HEAD
    #waitForCompletion: 'false' # Options: true, false
    #successCriteria: # Optional
```

::: moniker-end
