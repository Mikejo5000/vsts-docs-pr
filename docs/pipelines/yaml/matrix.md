---
title: Matrix execution | VSTS & TFS    
description: Learn how to use YAML to configure CI/CD for the app and platform of your choice.
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: fec59e80-66bd-442f-ac72-e435195d3227
ms.manager: douge
ms.author: alewis
author: ericsciple
ms.reviewer: macoope
ms.date: 07/17/2018
ms.topic: reference
monikerRange: '>= tfs-2018'
---

# Matrix execution

### Matrix

A `matrix` execution enables a phase to be dispatched multiple times, with different variable sets.

For example, a common scenario is to run the same build steps for varying permutations of architecture (x86/x64) and configuration (debug/release).

In the following example, different variables `buildArch` and `buildConfig` are added for each job that is dispatched.

```yaml
queue:
  parallel: 2 # Limit to two agents at a time
  matrix:
    x64_debug:
      buildArch: x64
      buildConfig: debug
    x64_release:
      buildArch: x64
      buildConfig: release
    x86_release:
      buildArch: x86
      buildConfig: release
steps:
- script: build arch=$(buildArch) config=$(buildConfig)
```

When combined with a matrix, the `parallel` property indicates the maximum number of jobs to run concurrently.
