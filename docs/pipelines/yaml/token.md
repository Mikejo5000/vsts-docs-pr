---
title: OAuth token for scripts | VSTS & TFS    
description: Learn how to use YAML to configure CI/CD for the app and platform of your choice.
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: 3477bf70-e26e-4188-acbd-8d19aed438c5
ms.manager: douge
ms.author: alewis
author: ericsciple
ms.reviewer: macoope
ms.date: 07/17/2018
ms.topic: reference
monikerRange: '>= tfs-2018'
---

# OAuth token for scripts

The OAuth token to communicate back to VSTS is available as a secret variable within a YAML build. The token can be use to authenticate to the [VSTS REST API](https://www.visualstudio.com/en-us/integrate/api/overview).

You can map the variable into the environment block for your script, or pass it via an input.

For example:

```yaml
steps:
- powershell: |
    # Definitions URL
    $url = "$($env:SYSTEM_TEAMFOUNDATIONCOLLECTIONURI)$env:SYSTEM_TEAMPROJECTID/_apis/build/definitions/$($env:SYSTEM_DEFINITIONID)?api-version=2.0"
    Write-Host "URL: $url"

    # Get the current definition
    $definition = Invoke-RestMethod -Uri $url -Headers @{
      Authorization = "Bearer $env:SYSTEM_ACCESSTOKEN" # OAuth token
    }

    # Output the result
    Write-Host "Definition = $($definition | ConvertTo-Json -Depth 100)"
  env:
    SYSTEM_ACCESSTOKEN: $(system.accesstoken) # Explicitly map the OAuth token.
                                              # Secret variables are not mapped into the
                                              # process environment block by default.
```
