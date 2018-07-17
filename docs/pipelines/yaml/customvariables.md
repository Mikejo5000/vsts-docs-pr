---
title: Custom variables | VSTS & TFS    
description: Learn how to use YAML to configure CI/CD for the app and platform of your choice.
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: 4f726adf-daf6-4926-b270-193132538a48
ms.manager: douge
ms.author: alewis
author: ericsciple
ms.reviewer: macoope
ms.date: 07/17/2018
ms.topic: reference
monikerRange: '>= tfs-2018'
---

# Custom variables

## Custom variables

Custom variables can be defined within the pipeline.

For example:

```yaml
# Set variables once
variables:
  configuration: debug
  platform: x64

steps:

# Build solution 1
- task: MSBuild@1
  inputs:
    solution: solution1.sln
    configuration: $(configuration) # Use the variable
    platform: $(platform)

# Build solution 2
- task: MSBuild@1
  inputs:
    solution: solution2.sln
    configuration: $(configuration) # Use the variable
    platform: $(platform)
```

## Defined in the web

Variables can also be defined centrally from the definition editor in the web, on the `Variables` tab.