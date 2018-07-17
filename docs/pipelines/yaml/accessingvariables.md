---
title: Accessing variables from scripts | VSTS & TFS    
description: Learn how to use YAML to configure CI/CD for the app and platform of your choice.
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: 9eb51664-b0dd-4a6b-ac40-5d6438acf4e5
ms.manager: douge
ms.author: alewis
author: ericsciple
ms.reviewer: macoope
ms.date: 07/17/2018
ms.topic: reference
monikerRange: '>= tfs-2018'
---

# Accessing variables from scripts

Pipeline variables are passed along to scripts, as process environment variables.

The variable name is transformed to upper case and the characters \".\" and \" " are replaced with \"_\".

Example for macOS and Linux:

```yaml
queue: Hosted Linux Preview
steps:
- script: |
    cd $AGENT_HOMEDIRECTORY
    ls
```

Example for Windows:

```yaml
queue: Hosted VS2017
steps:
- script: |
    cd %AGENT_HOMEDIRECTORY%
    dir
```

For a full list of variables, you can dump the environment variables from a script.

Example for macOS and Linux:

```yaml
queue: Hosted Linux Preview
steps:
- script: printenv | sort
```

Example for Windows:

```yaml
queue: Hosted VS2017
steps:
- script: set
```
