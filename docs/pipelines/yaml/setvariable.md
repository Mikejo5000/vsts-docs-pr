---
title: Setting variables from a script | VSTS & TFS    
description: Learn how to use YAML to configure CI/CD for the app and platform of your choice.
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: 78ac9478-2f66-4f16-8296-c064388d0354
ms.manager: douge
ms.author: alewis
author: ericsciple
ms.reviewer: macoope
ms.date: 07/17/2018
ms.topic: reference
monikerRange: '>= tfs-2018'
---

# Setting variables from a script

A new variable can be defined within a step, and can be accessed from a downstream step.

Example for macOS and Linux:

```yaml
queue: Hosted Linux Preview

steps:

# Create a variable
- script: |
    echo '##vso[task.setvariable variable=myVariable]abc123'

# Print the variable
- script: |
    echo my variable is $(myVariable)
```

Example for Windows:

```yaml
queue: Hosted VS2017

steps:

# Create a variable
- script: |
    echo ##vso[task.setvariable variable=myVariable]abc123

# Print the variable
- script: |
    echo my variable is $(myVariable)
```
