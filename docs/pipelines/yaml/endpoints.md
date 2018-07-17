---
title: Endpoints | VSTS & TFS    
description: Learn how to use YAML to configure CI/CD for the app and platform of your choice.
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: 41cafb06-16e6-43bb-b21e-dd86db44ff61
ms.manager: douge
ms.author: alewis
author: ericsciple
ms.reviewer: macoope
ms.date: 07/17/2018
ms.topic: reference
monikerRange: '>= tfs-2018'
---

# Endpoints

Endpoints can be specified by name. For example,

```yaml
queue: Hosted VS2017
steps:
- task: TODO@1
  inputs:
    subscription: MyAzureSubscription
```

Note, for rename resiliency, endpoints can be specified by their GUID instead of name.

For details about tasks, refer [here](tasks.md).

For details about endpoint authorization, refer [here](authz.md).
