---
title: Checkout options | VSTS & TFS    
description: Learn how to use YAML to configure CI/CD for the app and platform of your choice.
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: 4ae33ad5-ed75-4353-9027-54727acfba83
ms.manager: douge
ms.author: alewis
author: ericsciple
ms.reviewer: macoope
ms.date: 07/17/2018
ms.topic: reference
monikerRange: '>= tfs-2018'
---

# Checkout options

## Checkout step

The `checkout` step can be used to control the checkout options. The well-known \"self\" repo is the repo associated with the entry .yml file.

For example, the clean setting can be specified on the checkout step:

```yaml
steps:
- checkout: self
  clean: false
- script: echo hello world
```

## Skip checkout

To skip the checkout step, a `checkout: none` step must be added. When the list of steps does not contain a checkout step at all, a `checkout: self` step is implicitly added by the system.

```yaml
steps:
- checkout: none
- script: echo hello world
```

## Supported checkout options

```yaml
clean: true | false
fetchDepth: number
lfs: true | false
```
