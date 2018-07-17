---
title: Pipeline instance name | VSTS & TFS    
description: Learn how to use YAML to configure CI/CD for the app and platform of your choice.
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: 6c1412f0-7b51-4a65-bae9-8813646d7042
ms.manager: douge
ms.author: alewis
author: ericsciple
ms.reviewer: macoope
ms.date: 07/17/2018
ms.topic: reference
monikerRange: '>= tfs-2018'
---

# Pipeline instance name

The pipeline instance name can be specified using the `name` property.

For example:

```yaml
name: $(BuildDefinitionName)_$(Date:yyyyMMdd)$(Rev:.rr)
steps:
- script: echo hello world
```

[Refer here](https://docs.microsoft.com/en-us/vsts/build-release/concepts/definitions/build/options#build-number-format) for details about the pipeline instance name.
