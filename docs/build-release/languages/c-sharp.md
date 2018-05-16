---
title: CI for C#, F#, Visual Basic projects
description: Continuous integration for C#, F#, and Visual Basic projects
ms.assetid: 14698D5F-0613-4AD5-AB16-35877763888C
ms.prod: devops
ms.technology: devops-cicd
ms.topic: conceptual
ms.manager: douge
ms.author: alewis
author: andyjlewis
ms.date: 05/15/2018
monikerRange: '>= tfs-2015'
---

# CI for C#, F#, Visual Basic Projects

::: moniker range="vsts"

VSTS can automatically build your repositories containing C#, F#, or Visual Basic projects. Before reading the guidance on these languages, make sure to read the [web quickstart](../build/hello-world.md) or [YAML quickstart](../build/with-yaml.md) first.

::: moniker-end

::: moniker range="< vsts"

TFS can automatically build your repositories containing C#, F#, or Visual Basic projects. Before reading the guidance on these languages, make sure to read the [quickstart](../build/hello-world.md) first.

::: moniker-end

## Build tools

::: moniker range="vsts"

VSTS provides first class integration with a number of build environments including .NET, .NET Core, and Docker. You can run builds in VSTS without having to set up any infrastructure.

If you are building a Visual Studio solution, then you can use the [hosted agents](../concepts/agents/hosted.md) included with VSTS. They contain the latest released version of Visual Studio, or one of the earlier RTM versions. If you are building a .NET Core project, the hosted agents contain the latest release and several earlier releases of .NET Core SDK. To run a Docker build, you can use either the Windows hosted agents or Linux hosted agents. For a complete listing of the versions of build tools installed in VSTS, see [Hosted agents](../concepts/agents/hosted.md).

::: moniker-end

::: moniker range="< vsts"

TFS provides first class integration with a number of build environments including .NET, .NET Core, and Docker. You must first set up a private agent with the right version of the build tool you need by installing Visual Studio, .NET Core SDK, or Docker.

::: moniker-end

### .NET

# [Web](#tab/web)

Use one of the following templates as you set up CI for your project.

* .NET Desktop - This template can be used for any Visual Studio solution.
* ASP.NET - This template is similar to .NET Desktop, but it also packages the output into a web deploy package.

# [YAML](#tab/yaml)

::: moniker range="< vsts"

YAML is not supported in TFS.

::: moniker-end

::: moniker range="vsts"

Add the following to .vsts-ci.yml to build a .NET project.

```yaml
queue:
  name: Hosted VS2017

steps:
- task: NuGetToolInstaller@0
  inputs:
    versionSpec: 4.4.1

- task: NuGetCommand@2
  inputs:
    restoreSolution: '<solution name>'

- task: VSBuild@1
  inputs:
    solution: '<solution name>'
    platform: '<build platform>'
    configuration: '<build configuration>'
```

::: moniker-end
---