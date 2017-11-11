---
title: CI Build in code using YAML
description: Define your CI build process in YAML in Visual Studio Team Services (VSTS) and Team Foundation Server (TFS)
ms.prod: vs-devops-alm
ms.technology: vs-devops-build
ms.assetid: 5A3A363E-C21F-4593-A145-B57492E9FEDC
ms.manager: douge
ms.author: alewis
ms.date: 11/11/2017
---

# Configure your CI Build in code using YAML

**VSTS**

When it comes to your CI builds on VSTS, you've got a choice: define your process in a web-based interface, or, you can configure your CI process as code in a YAML build. YAML build definitions give you the advantages of _configuration as code_. 

One of the key advantages is that your CI process is versioned with your code. This means if someone changes your build process and something breaks, you can much more easily see and revert the change. It's just as easy to see and fix as any other kind of bug in your code because the process definition is versioned in your code.

> [!TIP]
> If you're new to YAML builds, or to VSTS, we suggest you [begin with our tutorial](build-yaml-get-started.md) and then come back here.

## How do YAML builds compare to web-interface builds?

[//]: # (TODO: review https://github.com/Microsoft/vsts-agent/blob/master/docs/preview/yamlgettingstarted-features.md with PM; brainstorm for other gaps)

|Capability|YAML|Web interface|
|-|-|-|
|<center>**Repository**</center>|
|Git and GitHub|Yes|Yes|
|TFVC|No|Yes|
|Bitbucket, external Git, Subversion|No|Yes|
|<center>**Capabilities**</center>|
|Fan out and fan in|Yes|No|
|Test and debug the process locally|Yes|No|
|Inline bash scripts|Yes|No|
