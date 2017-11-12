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

In a YAML definition, your CI build process is versioned with your code. This means: 

* If someone changes your build process and something breaks or works differently than you expect, you can much more easily identify the issue in the context of the rest of your codebase. This way you see and fix as any other kind of bug in your code because the process definition is versioned in your code.

* It's easier to copy and paste from one build definition into another.

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

## Automatic creation of YAML builds

[//]: # (TODO: on 11/12/17 test in OurAccount I found that it does not happen on import. correct? will this change? any other cases where it's created automatically?)

[//]: # (TODO: on 11/12/17 test in OurAccount I tried to delete definition and YAML file and and start over using same repo; seems that automatic no longer works in this case; is this by design?)

To make it more convenient to create YAML build definitions, VSTS automatically creates a definition when you add a file named .vsts-ci.yml to the root of your resository. It creates the build definition in a folder that has the same name as your repository.