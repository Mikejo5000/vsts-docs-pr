---
title: Azure web app for container deployment | Microsoft Docs
description: Deploy to Azure web app for container from VSTS or TFS
services: vsts
ms.prod: devops
ms.technology: devops-cicd
ms.topic: conceptual
manager: douge
ms.assetid:
ms.author: ahomer
author: alexhomer1
ms.date: 07/22/2018
monikerRange: '>= tfs-2017'
---

# Azure web app for containers

::: moniker range="<= tfs-2018"
[!INCLUDE [temp](../_shared/concept-rename-note.md)]
::: moniker-end

You can automatically deploy your containers to an Azure App Service after every successful build.

::: moniker range="tfs-2017"

> [!NOTE]
> 
> This guidance applies to TFS version 2017.3 and later.

::: moniker-end

::: moniker range="vsts"

> [!NOTE]
> To use YAML you must have the **Build YAML pipelines** [preview feature](/vsts/project/navigation/preview-features) enabled.

::: moniker-end

## Example

If you want some sample code that works with this guidance, follow these steps:

- Import (into VSTS or TFS) or fork (into GitHub) this repo:

```
https://github.com/adventworks/dotnetcore-sample

```
    
- Follow the guidance in [Docker](../languages/docker.md) to build the sample code.

- Create a web app for container in Azure portal. For the container, select the image that you pushed to Docker hub while following the example in the above doc.

- Set up continuous deployment to the web app for container using the following instructions:

# [Designer](#tab/designer)

Select Empty Template in a release definition. Add an Azure CLI task with inline script:

```bash
az webapp config container set --name <name of your web app> --resource-group <name of your resource group> --docker-registry-server-user <user id for Docker hub> --docker-registry-server-password <Password for Docker hub> --docker-custom-image-name $(Build.Repository.Name):$(Build.BuildId)'
```

# [YAML](#tab/yaml)

::: moniker range="vsts"

Add the following line to your `.vsts-ci.yml` file.

```yaml
- task: AzureCLI@1
  displayName: Azure CLI 
  inputs:
    azureSubscription: '<Name of your Azure subscription>'
    scriptLocation: inlineScript
    inlineScript: 'az webapp config container set --name <name of your web app> --resource-group <name of your resource group> --docker-registry-server-user <user id for Docker hub> --docker-registry-server-password <Password for Docker hub> --docker-custom-image-name $(Build.Repository.Name):$(Build.BuildId)'
```

::: moniker-end

::: moniker range="< vsts"

YAML builds are not yet available on TFS.

::: moniker-end

---

## Container registry

To deploy Docker images to Azure web apps, you need a container registry. You can either use Docker hub or Azure container registry.

### Docker hub

The following sequence of tasks can be used to continuously build, push, and deploy an image to web app via Docker hub.

# [Designer](#tab/designer)

- Docker task
    - Container registry type: `Container registry`
    - Docker registry service connection: <Your Docker hub service connection>
    - Action: `Build an image`
    - Qualify image name: `Checked`

- Docker task
    - Container registry type: `Container registry`
    - Docker registry service connection: <Your Docker hub service connection>
    - Action: `Push an image`
    - Qualify image name: `Checked`

- Azure CLI
    - Azure subscription: Your Azure service connection
    - Script location: inline
    - Inline script: `az webapp config container set --name <name of your web app> --resource-group <name of your resource group> --docker-registry-server-user <Docker id for Docker hub> --docker-registry-server-password <Password for Docker hub> --docker-custom-image-name $(Build.Repository.Name):$(Build.BuildId)`

# [YAML](#tab/yaml)

```yaml
steps:
- task: Docker@0
  displayName: Build an image
  inputs:
    containerregistrytype: 'Container Registry'
    dockerRegistryConnection: '<Name of your Docker hub service connection>'

- task: Docker@0
  displayName: Push an image
  inputs:
    containerregistrytype: 'Container Registry'
    dockerRegistryConnection: '<Name of your Docker hub service connection>'
    action: 'Push an image'


- task: AzureCLI@1
  displayName: Azure CLI 
  inputs:
    azureSubscription: '<Name of your Azure service connection>'
    scriptLocation: inlineScript
    inlineScript: 'az webapp config container set --name <name of your web app> --resource-group <name of your resource group> --docker-registry-server-user <Docker id for Docker hub> --docker-registry-server-password <Password for Docker hub> --docker-custom-image-name $(Build.Repository.Name):$(Build.BuildId)'
```
---

### Azure container registry

The following sequence of tasks can be used to continuously build, push, and deploy an image to web app via Azure container registry.

# [Designer](#tab/designer)

- Docker task
    - Container registry type: `Azure Container Registry`
    - Azure subscription: <Your Azure service connection>
    - Azure container registry: <Name of your registry>
    - Action: `Build an image`
    - Qualify image name: `Checked`

- Docker task
    - Container registry type: `Container registry`
    - Azure subscription: <Your Azure service connection>
    - Azure container registry: <Name of your registry>
    - Action: `Push an image`
    - Qualify image name: `Checked`

- Azure App Service Deploy
    - Task version: 4.*
    - Connection type: `Azure resource manager`
    - Azure subscription: <Your Azure service connection>
    - App service type: Web app for containers
    - App service name: <Name of your web app>
    - Registry or namespace: `<name of your registry>.azurecr.io`
    - Image: `$(Build.Repository.Name)`
    - Tag: `$(Build.BuildId)`

# [YAML](#tab/yaml)

```yaml
- task: Docker@0
  inputs:
    azureSubscription: '<Name of your Azure subscription>'
    azureContainerRegistry: '{"loginServer":"adventworks.azurecr.io", "id" : "/subscriptions/<Azure subscription id>/resourceGroups/<Resource group where your container registry is hosted>/providers/Microsoft.ContainerRegistry/registries/<Name of your registry>"}' # for example, "loginServer":"adventworks.azurecr.io", "id" : "/subscriptions/xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/adventworks/providers/Microsoft.ContainerRegistry/registries/adventworks"

- task: Docker@0
  inputs:
    azureSubscription: '<Name of your Azure subscription>'
    azureContainerRegistry: '{"loginServer":"adventworks.azurecr.io", "id" : "/subscriptions/<Azure subscription id>/resourceGroups/<Resource group where your container registry is hosted>/providers/Microsoft.ContainerRegistry/registries/<Name of your registry>"}' # for example, "loginServer":"adventworks.azurecr.io", "id" : "/subscriptions/xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/adventworks/providers/Microsoft.ContainerRegistry/registries/adventworks"
    action: 'Push an image'

- task: AzureRmWebAppDeployment@4
  inputs:
    azureSubscription: '<Name of your Azure subscription>'
    appType: webAppContainer
    WebAppName: '<Name of your web app>'
    DockerNamespace: <Name of your registry>.azurecr.io
    DockerRepository: '$(Build.Repository.Name)'
    DockerImageTag: '$(Build.BuildId)'

```
---

<a name="endpoint"></a>
## Azure service connection

The **Azure App Service Deploy** task, similar to other built-in Azure tasks, requires an Azure service connection as an
input. The Azure service connection stores the credentials to connect from VSTS or TFS to Azure. 

# [Designer](#tab/designer)

::: moniker range="vsts"

The easiest way to get started with this task is to be signed in as a user that owns both the VSTS and the Azure subscriptions.
In this case, you won't have to manually create the service connection.
Otherwise, to learn how to create an Azure service connection, see [Create an Azure service connection](../library/connect-to-azure.md).

::: moniker-end

::: moniker range="< vsts"

To learn how to create an Azure service connection, see [Create an Azure service connection](../library/connect-to-azure.md).

::: moniker-end

# [YAML](#tab/yaml)

::: moniker range="vsts"

You must supply an Azure service connection to the `AzureRmWebAppDeployment` task. The Azure service connection stores the credentials to connect from VSTS to Azure. See [Create an Azure service connection](../library/connect-to-azure.md).

::: moniker-end

::: moniker range="< vsts"

YAML builds are not yet available on TFS.

::: moniker-end

---

## Deploy to multiple web apps

# [Designer](#tab/designer)

If you want to deploy to multiple web apps, add environments to your release pipeline.
You can control the order of deployment. To learn more, see [Environments](../release/environments.md).

# [YAML](#tab/yaml)

::: moniker range="vsts"

You can use [phases](../process/phases.md) in your YAML file to set up a pipeline of deployments.
Using phases, you can control the order of deployment to multiple web apps.

```yaml
phases:

- phase: buildandtest
  queue: Hosted Linux Preview
  steps:

  # add steps here to build the app

  # the following will publish an artifact called drop
  - task: PublishBuildArtifacts@1

  - task: AzureRmWebAppDeployment@3
    inputs:
      azureSubscription: '<Test environment Azure service connection>'
      WebAppName: '<name of test environment web app>'

- phase: prod
  queue: Hosted Linux Preview
  dependsOn: buildandtest
  condition: succeeded()
  steps:

  # step to download the artifacts from the previous phase
  - task: DownloadBuildArtifacts@0
    inputs:
      artifactName: drop

  - task: AzureRmWebAppDeployment@3
    inputs:
      azureSubscription: '<Prod environment Azure service connection>'
      WebAppName: '<name of prod environment web app>'
```

::: moniker-end

::: moniker range="< vsts"

YAML builds are not yet available on TFS.

::: moniker-end

---

## CD settings on Azure web app

Explain the difference between using CD settings on the Azure web app vs setting up a pipeline with the Azure web app deployment task.

## Deploying conditionally

You may choose to deploy only certain builds to your Azure web app. 

# [Designer](#tab/designer)

In your release pipeline you can implement various checks and conditions to control the deployment.

* Set **branch filters** to configure the **continuous deployment trigger** on the artifact of the release pipeline.
* Set **pre-deployment approvals** as a pre-condition for deployment to an environment.
* Configure **gates** as a pre-condition for deployment to an environment.
* Specify conditions for a task to run.

To learn more, see [Release, branch, and environment triggers](../release/triggers.md), [Release deployment control using approvals](../release/approvals/approvals.md), [Release deployment control using gates](../release/approvals/gates.md), and [Specify conditions for running a task](../process/conditions.md).

# [YAML](#tab/yaml)

::: moniker range="vsts"

To do this in YAML, you can use one of these techniques:

* Isolate the deployment steps into a separate phase, and add a condition to that phase.
* Add a condition to the step.

The following example shows how to use step conditions to deploy only those builds that originate from master branch.

```yaml
- task: AzureRmWebAppDeployment@3
  condition: and(succeeded(), eq(variables['Build.SourceBranch'], 'refs/heads/master'))
  inputs:
    azureSubscription: '<Azure service connection>'
    WebAppName: '<Name of web app>'
```

To learn more about conditions, see [Specify conditions](../process/conditions.md). 

::: moniker-end

::: moniker range="< vsts"

YAML builds are not yet available on TFS.

::: moniker-end

---
