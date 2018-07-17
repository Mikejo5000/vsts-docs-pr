---
title: Macro syntax | VSTS & TFS    
description: Learn how to use YAML to configure CI/CD for the app and platform of your choice.
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: 8b5f3373-3fc1-4936-bfb6-5284b1b58d6b
ms.manager: douge
ms.author: alewis
author: ericsciple
ms.reviewer: macoope
ms.date: 07/17/2018
ms.topic: reference
monikerRange: '>= tfs-2018'
---

# Macro syntax

Within pipeline inputs, variables can be referenced using macro syntax.

Example for macOS and Linux:

```yaml
queue: Hosted Linux Preview
steps:
- script: ls
  workingDirectory: $(agent.homeDirectory)
```

Example for Windows:

```yaml
queue: Hosted VS2017
steps:
- script: dir
  workingDirectory: $(agent.homeDirectory)
```
