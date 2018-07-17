---
title: Slice execution | VSTS & TFS    
description: Learn how to use YAML to configure CI/CD for the app and platform of your choice.
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: 685877a5-d647-492d-91da-0421576e9f75
ms.manager: douge
ms.author: alewis
author: ericsciple
ms.reviewer: macoope
ms.date: 07/17/2018
ms.topic: reference
monikerRange: '>= tfs-2018'
---

# Slice execution

### Slice

A slice execution dispatches a phase N times, to enable dividing work among the jobs.

The `parallel` setting indicates how many jobs to dispatch.

Variables `system.sliceNumber` and `system.sliceCount` are added to each job. The variables can then be used within your scripts to divide work among the jobs.

```yaml
queue:
  parallel: 5
steps:
- script: test slice=$(system.sliceNumber) sliceCount=$(system.sliceCount)
```
