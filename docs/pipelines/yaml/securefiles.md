---
title: Secure files | VSTS & TFS    
description: Learn how to use YAML to configure CI/CD for the app and platform of your choice.
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: 9347fa69-fe43-4702-9bc7-30151d4e1668
ms.manager: douge
ms.author: alewis
author: ericsciple
ms.reviewer: macoope
ms.date: 07/17/2018
ms.topic: reference
monikerRange: '>= tfs-2018'
---

 # Secure files

Secure files can be referend by name, for example:

```yaml
queue: Hosted Linux Preview
steps:

# Download the secure file
- task: DownloadSecureFile@1
  name: mySecureFile
  inputs:
    secureFile: sample-secure-file.txt

# Dump the contents
- script: |
    cat $(mySecureFile.secureFilePath)
```

Note, for rename resiliency, secure files can be specified by their GUID instead of name.
