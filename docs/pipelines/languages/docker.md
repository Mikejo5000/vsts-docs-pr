---
title: Docker
description: Building Docker images using VSTS and TFS
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: 79DDAE0F-DAB6-4541-ACAF-88CD212C188F
ms.manager: douge
ms.author: alewis
author: andyjlewis
ms.reviewer: vijayma
ms.date: 07/05/2018
ms.topic: quickstart
monikerRange: '>= tfs-2017'
---

# Docker

This guidance explains how to build Docker container images. Before you read this topic, you should complete one of the quickstarts and create a basic build pipeline: [designer](../get-started-designer.md) or [YAML](../get-started-yaml.md).

::: moniker range="tfs-2017"

> [!NOTE]
> 
> This guidance applies to TFS version 2017.3 and newer.

::: moniker-end

::: moniker range="vsts"

> [!NOTE]
> To use YAML you must have the **Build YAML definitions** [preview feature](/vsts/project/navigation/preview-features) enabled on your account.

::: moniker-end

<br/>

> [!VIDEO https://www.youtube.com/embed/X4Puu0BS3GE]

## Example

If you want some sample code that works with this guidance, import (into VSTS or TFS) or fork (into GitHub) this repo:

```
https://github.com/adventworks/dotnetcore-sample
```

# [Designer](#tab/designer)

> [!NOTE]
> If you are new to creating build pipelines, then complete the [designer](../get-started-designer.md) quickstart first before following these instructions.

* After you have the sample code in your own repository, create a build definition and select the **ASP.NET Core** template. This automatically adds the tasks required to build the sample repository.
* Select **Process** under the **Tasks** tab of the build pipeline editor, and change its propertiesas follows:
  * **Agent queue:** `Hosted Linux Preview`
  * **Projects to test:** `**/*[Tt]ests/*.csproj`
* Modify the **.NET Core Publish** task in the build pipeline as follows:
  * **Arguments:** `--configuration $(BuildConfiguration) --output out`
  * **Zip published projects:**: Unchecked
* Remove the **Publish artifact** task.
* Add **Docker** task after the **.NET Core Publish** task and configure it as follows to build an image using the Dockerfile in the repository:
  * **Action:** `Build an image`
* Add another **Docker** task and configure it as follows to push the image to your Docker hub registry:
  * **Action:** `Push an image`
  * **Container registry type:** `Container registry`
  * **Docker registry connection:** Select `New` and create a connection to your Docker hub registry.

Save the pipeline and queue a build to see it in action. Then read through the rest of this topic to learn some of the more common changes people make to customize their Docker build.

# [YAML](#tab/yaml)

::: moniker range="vsts"

> [!NOTE]
> If you are new to creating build pipelines using YAML, then complete the [YAML](../get-started-yaml.md) quickstart first before following these instructions.

* The sample code above includes a `.vsts-ci.yml` file at the root of the repository. Replace the contents of this file with the following:

    ```yaml
    queue: 'Hosted Linux Preview'
    variables:
      buildConfiguration: 'Release'
    
    steps:
      - task: DotNetCoreCLI@2
        inputs:
          command: 'restore'
          projects: '**/*.csproj'
    
      - task: DotNetCoreCLI@2
        inputs:
          command: 'build'
          projects: '**/*.csproj'
          arguments: '--configuration $(buildConfiguration)'
    
      - task: DotNetCoreCLI@2
        inputs:
          command: 'test'
          projects: '**/*[Tt]ests/*.csproj'
          arguments: '--configuration $(buildConfiguration)'
    
      - task: DotNetCoreCLI@2
        inputs:
          command: 'publish'
          arguments: '--configuration $(buildConfiguration) --output out'
          zipAfterPublish: false
    
    # Replace adventworks in the following with the name of your docker id.
      - script: docker build -f Dockerfile -t adventworks/dotnetcore-sample .
    ```
    
* As mentioned in the above YAML snippet, make sure to change `adventworks` to the name of your Docker hub id.
    
Push the above change to master branch in your repository, and then run a build using this YAML file. Then read through the rest of this topic to learn some of the more common changes people make to customize a Docker build.

::: moniker-end

::: moniker range="< vsts"

YAML builds are not yet available on TFS.

::: moniker-end

---

## Build environment

::: moniker range="vsts"

You can use VSTS to build and push your Docker images without needing to set up any infrastructure of your own. You can build either Windows or Linux container images. The [Microsoft-hosted agents](../agents/hosted.md) in VSTS have Docker pre-installed on them. We frequently update the version of Docker on the hosted images. To know which version of Docker is installed, see [Microsoft-hosted agents](../agents/hosted.md).

# [Designer](#tab/designer)

In the build definition, select **Tasks**, then select the **Process** node, and finally select the **Agent queue** that you want to use.

# [YAML](#tab/yaml)

Add the following snippet to your `.vsts-ci.yml` file to select the appropriate agent queue:

```yaml
queue: 'Hosted Linux Preview' # other options - 'Hosted VS2017'
```

---

Use the **Hosted Linux Preview** agent queue to build Linux containers. When you use this queue, you get a fresh Linux virtual machine with each build. This virtual machine runs the [agent](../agents/agents.md) and acts as a Docker host. Tasks in your build do not directly run on the virtual machine. Instead, they run in a Microsoft-provided Docker container on the virtual machine. [Shared volumes](https://docs.docker.com/storage/volumes/) are used to faciliate communication between the virtual machine and the container. You can run docker commands as part of your build, since the `docker.sock` socket of the host is volume mounted in the container.

Use the **Hosted VS2017** agent queue to build Windows containers. When you use this queue, you get a fresh Windows Server 2016 virtual machine with each build. The virtual machine runs the [agent](../agents/agents.md) and acts as a Docker host. Some of the common images such as `microsoft/dotnet-framework`, `microsoft/aspnet`, `microsoft/aspnetcore-build`, `microsoft/windowsservercore`, and `microsoft/nanoserver` are pre-cached on this Docker host. Building new images from these images will therefore be faster.

> [!NOTE]
> Using Hosted VS2017 agents, you can only build Docker images with Windows Server 2016 as the container OS. You cannot build Docker images with Windows Server 1803 as the container OS since the host operating system on the virtual machines is Windows Server 2016.

> [!NOTE]
> We do not yet have a pool of Microsoft-hosted agents running Windows Server 1803. Until this is available, you can build Windows Server 1803 images using self-hosted agents.

You cannot use **Hosted Mac Preview** to build container images as Docker is not installed on these agents.

As an alternative to using Microsoft-hosted agents, you can set up a [self-hosted agent](../agents/agents.md#install) with Docker installed. This is particularly useful if you want to cache additional images on the Docker host, and further improve the performance of your builds.

::: moniker-end

::: moniker range="< vsts"

Your builds run on a [self-hosted agent](../agents/agents.md#install). Make sure that you have Docker installed on the agent.

::: moniker-end

## Build an image

You can build a Docker image by running a script with `docker build` command or by using **Docker** task.

# [Designer](#tab/designer)

1. Select **Tasks** in the build pipeline, select the phase that runs your build tasks, then select **+** to add a new task to that phase.

1. In the task catalog, find and add the **Docker** task.

1. Select the task and, for **Action**, select **Build an image**.

1. If your Dockerfile depends on an image that is present in an authenticated registry, for e.g., a private Docker registry or Azure Container Registry, then specify those properties in the **Container registry type** and the corresponding service connection.

# [YAML](#tab/yaml)

::: moniker range="vsts"
To run the docker command via a script, add the following snippet to `.vsts-ci.yml` file.
```yaml
steps:
- script: docker build -f <Dockerfile>
```

To run the docker command via a task, add the following snippet to `.vsts-ci.yml` file. This example also shows how to build an image that depends on another image from a protected registry.
```yaml
steps:
- task: Docker@0
  displayName: Build an image
  inputs:
    containerregistrytype: 'Container Registry'
    dockerRegistryConnection: 'Adventworks DockerHub'  # replace with your Docker hub service connection
```
::: moniker-end

::: moniker range="< vsts"
YAML builds are not yet available on TFS.
::: moniker-end

---


## Integrate with app build

You can build and test your app, before creating the Docker image, in two ways:

1. Use the build pipeline as the primary means to orchestrate building your code, running tests, and creating an image. In this approach, you leverage [tasks](../process/tasks.md) to build and test your code. This approach is useful if you want to:
  * leverage (in-built or Marketplace) tasks to define how you build and test your app
  * run tasks that require authentication via service endpoints (e.g., authenticated NuGet or npm feeds)
  * publish test results  
  To create an image, you run a `docker build` command at the end of your build pipeline. This requires a  `Dockerfile` to be present in your repository. The `Dockerfile` copies the results of your build into the container.

2. Use `Dockerfile` as the primary means to build your code and run tests. In this approach, there is a single step in your build pipeline to run `docker build`. The rest of the steps are orchestrated by the docker build process itself. It is common to use a [multi-stage docker build](https://docs.docker.com/develop/develop-images/multistage-build/) in this approach. The advantage of this approach is that your build process is entirely captured in your Dockerfile and it is portable between the development machine and any build system. However, you cannot leverage specific features of VSTS or TFS such as tasks, phases, or test analytics.

The instructions in the example above are based on the first approach. Following that example, you can observe that:

* **.NET Core** task is used to build, test, and publish the app
* Test results are published by the **.NET Core** task
* `docker build` command is invoked either through a task or a script at the end of the build pipeline.

For the second approach, create a Dockerfile at the root of your repository with the following contents:

```
# First stage of multi-stage build
FROM microsoft/aspnetcore-build:2.0 AS build-env
WORKDIR /app

# copy the contents of agent working directory on host to workdir in container
COPY . ./

# dotnet commands to build, test, and publish
RUN dotnet restore
RUN dotnet build -c Release
RUN dotnet test dotnetcore-tests/dotnetcore-tests.csproj -c Release
RUN dotnet publish -c Release -o out

# Second stage - Build runtime image
FROM microsoft/aspnetcore:2.0
WORKDIR /app
COPY --from=build-env /app/dotnetcore-sample/out .
ENTRYPOINT ["dotnet", "dotnetcore-docker-sample.dll"]
```

Then, set up a build pipeline using the following instructions.

# [Designer](#tab/designer)

1. Select **Tasks** in the build pipeline, remove all the tasks that you may have in the pipeline.
1. Add **Docker** task and configure its properties:
   * **Action:** Build an image

# [YAML](#tab/yaml)

::: moniker range="vsts"

Create a build pipeline using the following snippet in `.vsts-ci-yml` file:

```yaml
queue: 'Hosted Linux Preview'
variables:
  buildConfiguration: 'Release'

steps:
  - script: docker build -f Dockerfile.full -t adventworks/dotnetcore-sample .
```

::: moniker-end

::: moniker range="< vsts"

YAML builds are not yet available on TFS.

::: moniker-end

---

<a name="troubleshooting"></a>
## Troubleshooting

If you are able to build your image on your development machine, but are having trouble building it on VSTS or TFS, explore the following potential causes and corrective actions:

::: moniker range="vsts"

* Check that you are using the correct type of agents - Microsoft-hosted Linux or Microsoft-hosted Windows - to mimic the type of containers you build on your development machine.

* If you use Microsoft-hosted agents to run your builds, the docker images are not cached from build to build since you get a new machine for every build. This will make your builds on Microsoft-hosted agents run longer than those on your development machine.

::: moniker-end

* Check that the versions of the .NET Core SDK and runtime on your development machine match those on the agent.
  You can include a command line script `dotnet --version` in your build definition to print the version of .NET Core SDK.
  Either use the **.NET Core Tool Installer** (as explained in this guidance) to deploy the same version on the agent,
  or update your projects and development machine to the newer version of .NET Core SDK.

* You may be using some logic in Visual Studio IDE that is not encoded in your build definition.
  VSTS or TFS run each of the commands you specify in the tasks one after the other in a new process.
  Look at the logs from the VSTS or TFS build to see the exact commands that ran as part of the build.
  Repeat the same commands in the same order on your development machine to locate the problem.

* If you have a mixed solution that includes some .NET Core projects and some .NET Framework projects,
  you should also use the **NuGet** task to restore packages specified in `package.json` files.
  Similarly, you should add **MSBuild** or **Visual Studio Build** tasks to build the .NET Framework projects.

* If your builds fail intermittently while restoring packages, either Nuget.org is having issues or there are
  networking problems between the Azure data center and Nuget.org. These are not under our control, and you may
  need to explore whether using VSTS Package Management with Nuget.org as an upstream source improves the reliability
  of your builds.

* Occasionally, when we roll out an update to the hosted images with a new version of .NET Core SDK or Visual Studio,
  something may break your build. This can happen, for example, if a newer version or feature of the NuGet tool
  is shipped with the SDK. To isolate these problems, use the **.NET Core Tool Installer** task to specify the version
  of the .NET Core SDK used in your build.

## Q&A

### Where can I learn more about the VSTS and TFS Package Management service?

[Package Management in VSTS and TFS](../../package/index.md)

### Where can I learn more about .NET Core commands?

[.NET Core command-line interface (CLI) tools](/dotnet/core/tools/)

### Where can I learn more about running tests in my solution?

[Unit testing in .NET Core projects](/dotnet/core/testing/)

### Where can I learn more about tasks?

[Build and release tasks](../tasks/index.md)
