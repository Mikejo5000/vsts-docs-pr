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

VSTS can automatically build your repositories containing C#, F#, or Visual Basic projects. Before reading the guidance on these languages, make sure to read the [web quickstart](../build/with-web.md) or [YAML quickstart](../build/with-yaml.md) first.

::: moniker-end

::: moniker range="< vsts"

TFS can automatically build your repositories containing C#, F#, or Visual Basic projects. Before reading the guidance on these languages, make sure to read the [quickstart](../build/with-web.md) first.

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


If you are building a Java application, use the following snippet to deploy the web archive (.war).
```yaml
- task: AzureRmWebAppDeployment@3
  inputs:
    azureSubscription: '<Azure service endpoint?'
    WebAppName: '<Name of web app>'
    Package: '$(System.DefaultWorkingDirectory)/**/*.war'
```

If you are building a Node app, then use the following snippet. It generates a web.config file during deployment and starts iisnode handler on the Azure web app.
```yaml
- task: AzureRmWebAppDeployment@3
  inputs:
    azureSubscription: '<Azure service endpoint>'
    WebAppName: '<Name of web app>'
    Package: '$(System.DefaultWorkingDirectory)'
    GenerateWebConfig: true
    WebConfigParameters: '-Handler iisnode -NodeStartFile server.js -appType node'
```

## Azure service endpoint

The **Azure App Service Deploy** task is the primary mechanism used in the above YAML snippets to deploy your web app to Azure. This task, similar to other built-in Azure tasks, requires an Azure service endpoint as an input. The Azure service endpoint stores the credentials to connect from VSTS to Azure. For more information about creating an Azure service endpoint in VSTS, see the topic _Create an Azure service endpoint_.

## Deploying to a virtual application

By default, you deployment happens to the root application in the Azure web app. You can deploy to a specific virtual application using the following:

```yaml
- task: AzureRmWebAppDeployment@3
  inputs:
    VirtualApplication: '<name of virtual application>'
```

## Deploying to a slot

You can configure the Azure web app to have multiple slots. Slots allow you to safely deploy your app and test it, before making it available to your customers.

The following example shows how to deploy to a staging slot, and then swap to production slot.

```yaml
- task: AzureRmWebAppDeployment@3
  inputs:
    azureSubscription: '<Azure service endpoint>'
    WebAppName: '<name of web app>'
    DeployToSlotFlag: true
    ResourceGroupName: '<name of resource group>'
    SlotName: staging

- task: AzureAppServiceManage@0
  inputs:
    azureSubscription: '<Azure service endpoint>'
    WebAppName: '<name of web app>'
    ResourceGroupName: '<name of resource group>'
    SourceSlot: staging
```

## Multiple web apps in a pipeline

You can use [phases](../concepts/process/phases.md) in your YAML file to set up a pipeline of deployments. Using phases, you can control the order of deployment to multiple web apps.

```yaml
phases:
- phase: test
  steps:
    - task: AzureRmWebAppDeployment@3
        inputs:
          azureSubscription: '<Test environment Azure service endpoint>'
          WebAppName: '<name of test environment web app>'

- phase: prod
  dependsOn: test
  steps:
    - task: AzureRmWebAppDeployment@3
        inputs:
          azureSubscription: '<Prod environment Azure service endpoint>'
          WebAppName: '<name of prod environment web app>'
```

## Configuration changes

You may want to apply a specific configuration for your web app before deploying to it. This is particularly useful when you deploy the same build to multiple web apps in a pipeline. For example, if your `Web.config` file contains a connection string named `connectionString` then, you can change its value prior to deploying to each web app. You can do this either by applying a web config transformation or by substituting variables in Web.config file. The following snippet shows an example of variable substitution.

```yaml
phases:
- phase: test
  variables:
    connectionString: <test-environment connection string>
  steps:
    - task: AzureRmWebAppDeployment@3
        inputs:
          azureSubscription: '<Test environment Azure service endpoint>'
          WebAppName: '<name of test environment web app>'
          enableXmlVariableSubstitution: true

- phase: prod
  dependsOn: test
  variables:
    connectionString: <prod-environment connection string>
  steps:
    - task: AzureRmWebAppDeployment@3
        inputs:
          azureSubscription: '<Prod environment Azure service endpoint>'
          WebAppName: '<name of prod environment web app>'
          enableXmlVariableSubstitution: true
```

## Deploying conditionally

You may choose to deploy only certain builds to the Azure web app. To do this, you can use one of these techniques:

* Isolate the deployment steps into a separate phase, and add a [condition](../concepts/process/conditions.md) to that phase.
* Add a condition to the step.

 The following example shows how to use step conditions to deploy only those builds that originate from master branch.

```yaml
- task: AzureRmWebAppDeployment@3
  condition: and(succeeded(), eq(variables['Build.SourceBranch'], 'refs/heads/master'))
  inputs:
    azureSubscription: '<Azure service endpoint>'
    WebAppName: '<Name of web app>'
```

## Deployment mechanisms

[!INCLUDE [include](_shared/azure-deployment-mechanisms-webapp.md)]

::: moniker-end
---
