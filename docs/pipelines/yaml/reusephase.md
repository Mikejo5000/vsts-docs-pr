---
title: Phase reuse | VSTS & TFS    
description: Learn how to use YAML to configure CI/CD for the app and platform of your choice.
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: efb2e76a-2679-49b5-bb7e-81f3474eebc3
ms.manager: douge
ms.author: alewis
author: ericsciple
ms.reviewer: macoope
ms.date: 07/17/2018
ms.topic: reference
monikerRange: '>= tfs-2018'
---

# Phase reuse

In the following example, a phase template is used to build across multiple platforms

```yaml
# File: phases/build.yml

parameters:
  name: ''
  queue: ''
  sign: false

phases:
- phase: ${{ parameters.name }}
  queue: ${{ parameters.queue }}
  steps:
  - script: npm install
  - script: npm test
  - ${{ if eq(parameters.sign, 'true') }}:
    - script: sign
```

```yaml
# File: .vsts-ci.yml

phases:
- template: phases/build.yml  # Template reference
  parameters:
    name: macOS
    queue: Hosted macOS Preview

- template: phases/build.yml  # Template reference
  parameters:
    name: Linux
    queue: Hosted Linux Preview

- template: phases/build.yml  # Template reference
  parameters:
    name: Windows
    queue: Hosted VS2017
    sign: true  # Extra step on Windows only
```

For details about parameter syntax, refer [here](templateexpressions.md).
