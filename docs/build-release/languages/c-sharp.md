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

# [Web](#tab/web)

Use one of the following templates as you set up CI for your project.

* .NET Desktop - This template can be used for any Visual Studio solution.
* ASP.NET - This template is similar to .NET Desktop, but it also packages the output into a web deploy package.
* ASP.NET Core - This template builds ASP.NET Core applications targeting .NET Core.
* ASP.NET Core (.NET Framework) - Use this to build ASP.NET Core applications targeting full .NET framework.

Each of these templates has tasks to restore the dependent packages from a package feed, build the project, run unit tests and publish test results, package the output in the case of web applications, and publish the output as an artifact.

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

Add the following to .vsts-ci.yml to build a .NET Core project.

```yaml
queue: Hosted VS2017

variables:
  BuildProjects: '**/*.csproj'
  BuildConfiguration: release

steps:
- task: DotNetCoreCLI@2
  inputs:
    command: restore
    projects: '$(BuildProjects)'

- task: DotNetCoreCLI@2
  inputs:
    projects: '$(BuildProjects)'
    arguments: '--configuration $(BuildConfiguration)'
```

::: moniker-end
---

## Restoring dependencies

Use the NuGet tool to restore dependencies for your .NET projects. Since there are several changes from one version of NuGet to another, it is recommended that you control the specific version of NuGet tool you use in your build pipeline through the use of [NuGet tool installer task](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/NuGetToolInstallerV0). This task allows you to specify the version of NuGet tool that must be installed on the agent, if it is not already present.

The [NuGet task](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/NuGetV0) restores all the dependencies in your project. This task supports reading the dependency information from the projects in your solution, packages.config, or project.json. The packages can be restored from NuGet.org, from VSTS package management service, or from another feed that you specify. You can specific a custom configuration by checking in a NuGet.config file into your repository.

For more information about restoring NuGet packages, see [Restore Package Management NuGet Packages in Build](../packages/nuget-restore.md).

Use the [Dotnet task](../tasks/build/dotnet-core.md) with `restore` option to restore dependencies for your .NET Core projects. The packages can be restored from NuGet.org, from VSTS package management service, or from another feed that you specify. You can specific a custom configuration by checking in a NuGet.config file into your repository.

## Unit testing

## Publishing symbols

## Packaging outputs

## Publishing artifacts

## Project type specific considerations

### WPF projects

### Database projects

### SSRS/SSIS projects
