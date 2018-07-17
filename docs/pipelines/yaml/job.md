---
title: Phase options | VSTS & TFS    
description: Learn how to use YAML to configure CI/CD for the app and platform of your choice.
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: 1e1b003d-4031-4b9b-9ae0-5a0dd9e9063f
ms.manager: douge
ms.author: alewis
author: ericsciple
ms.reviewer: macoope
ms.date: 07/17/2018
ms.topic: reference
monikerRange: '>= tfs-2018'
---

# Phase options

## Continue on error

When `continueOnError` is set to true and the phase fails, the phase result will be \"Succeeded with issues\" instead of "Failed\".

## Timeout

The `timeoutInMinutes` allows a limit to be set for the job execution time. When not specified, the default is 60 minutes.

The `cancelTimeoutInMinutes` allows a limit to be set for the job cancel time. When not specified, the default is 5 minutes.

The schema is:

```yaml
queue:
  timeoutInMinutes: number
  cancelTimeoutInMinutes: number
```

and:

```yaml
server:
  timeoutInMinutes: number
  cancelTimeoutInMinutes: number
```

## Variables

Variables can be specified on a phase. Refer [here](index.md#variables) for more information about variables.
