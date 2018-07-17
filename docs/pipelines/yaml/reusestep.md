---
title: Step reuse | VSTS & TFS    
description: Learn how to use YAML to configure CI/CD for the app and platform of your choice.
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: cb8c86ca-2516-41b2-8051-1b2bfe5c1604
ms.manager: douge
ms.author: alewis
author: ericsciple
ms.reviewer: macoope
ms.date: 07/17/2018
ms.topic: reference
monikerRange: '>= tfs-2018'
---

# Step reuse

Templates enable steps to be defined once, and used from multiple places.

In the following example, the same steps are used across multiple phases.

```yaml
# File: steps/build.yml

steps:
- script: npm install
- script: npm test
```

```yaml
# File: .vsts-ci.yml

phases:
- phase: macOS
  queue: Hosted macOS Preview
  steps:
  - template: steps/build.yml # Template reference

- phase: Linux
  queue: Hosted Linux Preview
  steps:
  - template: steps/build.yml # Template reference

- phase: Windows
  queue: Hosted VS2017
  steps:
  - template: steps/build.yml # Template reference
  - script: sign              # Extra step on Windows only
```
