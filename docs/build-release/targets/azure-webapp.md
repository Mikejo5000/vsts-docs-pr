---
title: Azure web app deployment
description: Deploy to an Azure web app from VSTS or TFS
ms.assetid: EE83B03F-19D7-4C96-84D9-7D86F808B61A
ms.prod: devops
ms.technology: devops-cicd
ms.topic: conceptual
ms.manager: douge
ms.author: ahomer
author: alexhomer1
ms.date: 05/10/2018
monikerRange: '>= tfs-2017'
---

# Azure web app deployment

::: moniker range="vsts"

VSTS can automatically deploy your web packages to Azure web app after every successful build.

::: moniker-end

::: moniker range="< vsts"

TFS can automatically deploy your web packages to Azure web app after every successful build.

::: moniker-end

# [Web](#tab/web)

The simplest way to deploy to an Azure web app is by creating a release pipeline using the correct template. Templates exist for apps developed in various programming languages. If you cannot find a template for your language, use the generic `Azure App Service Deployment` template.

## Azure service endpoint

The **Azure App Service Deploy** task is the primary mechanism to deploy your web app to Azure. This task, similar to other built-in Azure tasks, requires an Azure service endpoint as an input. The Azure service endpoint stores the credentials to connect from VSTS to Azure. For more information about creating an Azure service endpoint in VSTS, see the topic _Create an Azure service endpoint_.

## Deploying to a virtual application

By default, your deployment happens to the root application in the Azure web app. Instead, you can choose to deploy to a specific virtual application by typing its name in the `Virtual Application` property of `Azure App Service Deploy` task.

## Deploying to a slot

You can configure the Azure web app to have multiple slots. Slots allow you to safely deploy your app and test it, before making it available to your customers. Use the option to `Deploy to Slot` in `Azure App Service Deploy` task to specify the slot to deploy to. You can swap the slots by using the `Azure App Service Manage` task.

## Multiple web apps in a pipeline

You can use environments in your release pipeline to deploy to multiple web apps while controlling the order of deployment.

## Configuration changes

You may want to apply a specific configuration for your web app before deploying to it. This is particularly useful when you deploy the same build to multiple web apps in a pipeline. For example, if your `Web.config` file contains a connection string named `connectionString` then, you can change its value prior to deploying to each web app. You can do this either by applying a web config transformation or by substituting variables in Web.config file. To change the `connectionString` using variable substitution, follow these steps:

1. Create a release pipeline with two environments.
1. Link the artifact of the release pipeline to the build that produces the web package.
1. Define `connectionString` as a variable in each of the environments. Set the appropriate value.
1. Check the `XML variable substitution` option under `File Transforms and Variable Substitution Options` of `Azure App Service Deploy` task.

## Deploying conditionally

You may choose to deploy only certain builds to the Azure web app. Release pipelines support various checks and conditions to control the deployment.

* Set _Branch filters_ when configuring the continuous deployment trigger on the artifact of the release pipeline.
* Set _Pre-deployment approvals_ as a pre-condition for deployment to an environment.
* Configure _Gates_ as a pre-condition for deployment to an environment.
* Set [conditions](../concepts/process/conditions.md) on the task.

## Deployment mechanisms

[!INCLUDE [include](_shared/azure-deployment-mechanisms-webapp.md)]

# [YAML](#tab/yaml)

::: moniker range="< vsts"

YAML is not supported in TFS.

::: moniker-end

::: moniker range="vsts"

To deploy a web deploy package (.zip) to an Azure web app, add the following snippet to your .vsts-ci.yml file.

```yaml
- task: AzureRmWebAppDeployment@3
  inputs:
    azureSubscription: '<Azure service endpoint>'
    WebAppName: '<Name of web app>'
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
