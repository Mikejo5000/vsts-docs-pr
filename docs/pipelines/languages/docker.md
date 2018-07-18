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

This guidance explains how to build Docker images.

::: moniker range="vsts"

> [!NOTE]
> To use YAML you must have the **Build YAML definitions** [preview feature](/vsts/project/navigation/preview-features) enabled on your account.

::: moniker-end

::: moniker range="<= tfs-2018"
[!INCLUDE [temp](../_shared/concept-rename-note.md)]
::: moniker-end

::: moniker range="tfs-2017"

> [!NOTE]
> 
> This guidance applies to TFS version 2017.3 and newer.

::: moniker-end

<br/>

> [!VIDEO https://www.youtube.com/embed/X4Puu0BS3GE]

## Example

If you want some sample code that works with this guidance, import (into VSTS or TFS) or fork (into GitHub) this repo:

```
https://github.com/adventworks/dotnetcore-sample
```

To build a Docker image, you need a **Dockerfile**. The sample code contains a Dockerfile you can use with these instructions.

# [Designer](#tab/designer)

> [!IMPORTANT]
> If you are new to creating build pipelines, then complete the [designer](../get-started-designer.md) quickstart first before following these instructions.

::: moniker range="< vsts"
> [!NOTE]
> This scenario works on TFS, but some of the following instructions might not exactly match the version of TFS that you are using. Also, you'll need to set up a self-hosted agent, possibly also installing software. If you are a new user, you might have a better learning experience by trying this procedure out first using a [free VSTS account](https://go.microsoft.com/fwlink/?LinkId=307137).
::: moniker-end

1. After you have the sample code in your own repository, create a build pipeline and select the **ASP.NET Core** template. This automatically adds the tasks that you typically need to build an ASP.NET Core app.

1. Select **Process** under the **Tasks** tab of the build pipeline editor, and change its properties as follows:
  * **Agent queue:** `Hosted Linux`
  * **Projects to test:** `**/*[Tt]ests/*.csproj`

1. Modify the **.NET Core Publish** task in the build pipeline as follows:
  * **Arguments:** `--configuration $(BuildConfiguration) --output out`
  * **Zip published projects:** Unchecked
  * **Add project name to publish path:** Unchecked

1. Remove the **Publish artifact** task.

1. Add **Docker** task after the **.NET Core Publish** task and configure it as follows to build an image using the **Dockerfile** in the repository:
  * **Action:** `Build an image`

1. Add another **Docker** task and configure it as follows to push the image to your Docker hub registry:
  * **Action:** `Push an image`
  * **Container registry type:** `Container registry`
  * **Docker registry connection:** Select `New` and create a connection to your Docker hub registry.

Save the pipeline and queue a build to see it in action. 

# [YAML](#tab/yaml)

::: moniker range="vsts"

> [!IMPORTANT]
> If you are new to creating build pipelines using YAML, then complete the [YAML](../get-started-yaml.md) quickstart first before following these instructions.

The sample code above includes a `.vsts-ci.yml` file at the root of the repository. Replace the contents of this file with the following:

```yaml
queue: 'Hosted Linux'
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
    
# Replace adventworks in the following with the name of your Docker id.
- script: docker build -f Dockerfile -t adventworks/dotnetcore-sample .
```
    
As mentioned in the above YAML snippet, make sure to change `adventworks` to the name of your Docker hub id.
    
Push the above change to master branch in your repository, and then run a build using this YAML file to see it in action.

::: moniker-end

::: moniker range="< vsts"

YAML builds are not yet available on TFS.

::: moniker-end

---

Now that you've run a Docker build pipeline, you're ready to learn some of the more common changes people make to customize their Docker build.

## Build environment

::: moniker range="vsts"

You can use VSTS to build and push your Docker images without needing to set up any infrastructure of your own. You can build either Windows or Linux container images. The [Microsoft-hosted agents](../agents/hosted.md) in VSTS have Docker pre-installed on them. We frequently update the version of Docker on these agent machines. To know which version of Docker is installed, see [Microsoft-hosted agents](../agents/hosted.md).

# [Designer](#tab/designer)

In the build pipeline, select **Tasks**, then select the **Process** node, and finally select the **Agent queue** that you want to use.

# [YAML](#tab/yaml)

Add the following snippet to your `.vsts-ci.yml` file to select the appropriate agent queue:

```yaml
queue: 'Hosted Linux' # other options - 'Hosted VS2017'
```

---

### Microsoft-hosted Linux agents

Use the **Hosted Linux** agent queue to build Linux container images. When you use this queue, you get a fresh Linux virtual machine with each build. This virtual machine runs the [agent](../agents/agents.md) and acts as a Docker host. Tasks in your build do not directly run on the virtual machine at present. Instead, they run in a Microsoft-provided Docker container on the virtual machine. [Shared volumes](https://docs.docker.com/storage/volumes/) are used to faciliate communication between the virtual machine and the container. You can run Docker commands as part of your build, since the `docker.sock` socket of the host is volume mounted in the container.

You cannot use **Hosted Mac** to build container images as Docker is not installed on these agents.

### Microsoft-hosted VS2017 (Windows) agents

Use the **Hosted VS2017** agent queue to build Windows container images. When you use this queue, you get a fresh Windows Server 2016 virtual machine with each build. The virtual machine runs the [agent](../agents/agents.md) and acts as a Docker host. Some of the common images such as `microsoft/dotnet-framework`, `microsoft/aspnet`, `microsoft/aspnetcore-build`, `microsoft/windowsservercore`, and `microsoft/nanoserver` are pre-cached on this Docker host. Building new images from these images will therefore be faster.

> [!NOTE]
> * Using Hosted VS2017 agents, you can only build Docker images with Windows Server 2016 as the container OS. You cannot build Docker images with Windows Server 1803 as the container OS since the host operating system on the virtual machines is Windows Server 2016.
> * We do not yet have a pool of Microsoft-hosted agents running Windows Server 1803. Until this is available, you can build Windows Server 1803 images using self-hosted agents.

### Self-hosted agents

As an alternative to using Microsoft-hosted agents, you can set up [self-hosted agents](../agents/agents.md#install) with Docker installed. This is particularly useful if you want to cache additional images on the Docker host, and further improve the performance of your builds.

::: moniker-end

::: moniker range="< vsts"

Your builds run on a [self-hosted agent](../agents/agents.md#install). Make sure that you have Docker installed on the agent.

::: moniker-end

## Build an image

You can build a Docker image by running the `docker build` command in a script or by using the **Docker** task.

# [Designer](#tab/designer)

1. Select **Tasks** in your build pipeline, and then add the **Docker** task to the phase.

1. Select the task, and then for **Action**, select **Build an image**.

1. If your _Dockerfile_ depends on an image that is present in an authenticated registry (for example, a private Docker registry or Azure Container Registry), then specify those properties in the **Container registry type** and the corresponding service connection.

# [YAML](#tab/yaml)

::: moniker range="vsts"

To run the command in a script, add the following snippet to your `.vsts-ci.yml` file.

```yaml
steps:
- script: docker build -f <Dockerfile>
```

To use a task to run the command, add the following snippet to your `.vsts-ci.yml` file.

```yaml
steps:
- task: Docker@0
  displayName: Build an image
  inputs:
    containerregistrytype: 'Container Registry'
    dockerRegistryConnection: 'Adventworks DockerHub'  # replace with your Docker hub service connection
```

The above example also shows how to build an image that depends on another image from a protected registry.

::: moniker-end

::: moniker range="< vsts"
YAML builds are not yet available on TFS.
::: moniker-end

---

## Integrate with app build

Often you'll want to build and test your app before creating the Docker image. You can orchestrate this process either in your build pipeline or in your _Dockerfile_.

### Orchestrate in your build pipeline

In this approach, you use the build pipeline as the primary means to orchestrate building your code, running tests, and creating an image. This approach is useful if you want to:

* leverage (in-built or Marketplace) tasks to define how you build and test your app
* run tasks that require authentication via service endpoints (e.g., authenticated NuGet or npm feeds)
* publish test results  

To create an image, you run a `docker build` command at the end of your build pipeline. The **Dockerfile** contains the instructions to copy the results of your build into the container.

The instructions in the example section above demonstrate this approach.

### Orchestrate in your Dockerfile

In this approach, you use **Dockerfile** as the primary means to build your code and run tests. The build pipeline has a single step to run `docker build`. The rest of the steps are orchestrated by the Docker build process itself. It is common to use a [multi-stage Docker build](https://docs.docker.com/develop/develop-images/multistage-build/) in this approach. The advantage of this approach is that your build process is entirely captured in your **Dockerfile** and it is portable between the development machine and any build system. However, you cannot leverage specific features of VSTS or TFS such as tasks, phases, or test analytics.

To follow this approach, create a **Dockerfile** at the root of your repository with the following contents:

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
ENTRYPOINT ["dotnet", "dotnetcore-sample.dll"]
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
queue: 'Hosted Linux'
steps:
  - script: docker build -f Dockerfile -t adventworks/dotnetcore-sample .
```

::: moniker-end

::: moniker range="< vsts"

YAML builds are not yet available on TFS.

::: moniker-end

---

## Push an image

Once built, you can push the Docker image by using **Docker** task. You can push the image to a Docker registry or to Azure Container Registry (ACR). The **Docker** task sets up an authenticated connection to your registry or ACR making it easy for you to push your image.

# [Designer](#tab/designer)

1. Select **Tasks** in the build pipeline, select the phase that runs your build tasks, then select **+** to add a new task to that phase.

1. In the task catalog, find and add the **Docker** task.

1. Select the task and, for **Action**, select **Push an image**.

1. Specify how to connect to your registry in the **Container registry type** and the corresponding service connection properties.

# [YAML](#tab/yaml)

::: moniker range="vsts"
To push a Docker image, add the following snippet to `.vsts-ci.yml` file.
```yaml
steps:
- task: Docker@0
  displayName: Push an image
  inputs:
    containerregistrytype: 'Container Registry'
    dockerRegistryConnection: 'Adventworks DockerHub'   # replace with your Docker hub service connection
    action: 'Push an image'
```
::: moniker-end

::: moniker range="< vsts"
YAML builds are not yet available on TFS.
::: moniker-end

---

By default, this task tags your image as `<Docker id>/<repo name>:<build id>`

## Use docker-compose

Docker-compose allows you to bring up multiple containers and run tests. For example, you can use a docker-compose file to define two containers that need to work together to test your application - a web service containing your application and a test driver. You can build new container images every time you push a code change. You can wait for the test driver to finish running tests before bringing down the two containers.

::: moniker range="vsts"

If you use Microsoft-hosted agents, you do not have to run any additional steps to install and use docker-compose.

::: moniker-end

To extend the example using docker-compose, follow these steps:

Add a file `docker-compose.yml` at the root of your repository.

```yaml
sut:
  build: .
  dockerfile: Dockerfile.test
  links:
    - web
web:
  build: .
  dockerfile: Dockerfile
```
    
Add a file `Dockerfile.test` at the root of your repository.

```
FROM ubuntu:trusty
RUN apt-get update && apt-get install -yq curl && apt-get clean
WORKDIR /app
ADD test.sh /app/test.sh
CMD ["bash", "test.sh"]
```

Add a file `test.sh` at the root of your repository.

```
sleep 5
if curl web | grep -q 'ASP.NET Core '; then
  echo "Tests passed!"
  exit 0
else
  echo "Tests failed!"
  exit 1
fi
```

# [Designer](#tab/designer)

In the build pipeline, add a **Bash** task with the following inline script:

```
docker-compose -f docs/docker-compose.yml --project-directory . -p docs up -d
docker wait docs_sut_1
docker-compose -f docs/docker-compose.yml --project-directory . down
```

# [YAML](#tab/yaml)

::: moniker range="vsts"
Add the following snippet to your `.vsts-ci.yml` file.

```yaml
- script: |
    docker-compose -f docs/docker-compose.yml --project-directory . -p docs up -d |
    docker wait docs_sut_1 |
    docker-compose -f docs/docker-compose.yml --project-directory . down |
```
::: moniker-end

::: moniker range="< vsts"
YAML builds are not yet available on TFS.
::: moniker-end
---

::: moniker range="vsts"
> [!NOTE]
> When using Hosted Linux agents, the agent runs inside a container. The network of this container is not bridged to the network of the containers that you spin up through docker compose. As a result, you cannot communicate from the agent to one of the containers in the composition, for e.g., to drive tests. One way to tackle this is to explicitly create another test driver as a container within the composition, as we did in the example above. Another way to solve this is to use `docker-compose exec` and target a specific container in the composition from your script.
:::moniker-end

::: moniker range="vsts"
## Build ARM containers

When you use Hosted Linux agents, you create Linux container images for the amd64 architecture. To create images of other architectures (x86, ARM, etc), you can use a machine emulator such as [QEMU](https://www.qemu.org/). The following steps illustrate how to create an ARM container image:

Author your Dockerfile so that an Intel binary of QEMU exists in the base Docker image. For example, the Raspbian Docker image from [Resin](https://resin.io/) already has this.

```
FROM resin/rpi-raspbian
```

Run the following script in your build pipeline.

```
# register QEMU binary - this can be done by running the following Docker image
docker run --rm --privileged multiarch/qemu-user-static:register --reset
# build your image
docker build -t <your-image-tag> .
```

:::moniker-end

<a name="troubleshooting"></a>
## Troubleshooting

If you are able to build your image on your development machine, but are having trouble building it on VSTS or TFS, explore the following potential causes and corrective actions:

::: moniker range="vsts"

* Check that you are using the correct type of agents - Microsoft-hosted Linux or Microsoft-hosted Windows - to mimic the type of container images you build on your development machine.

* If you use Microsoft-hosted agents to run your builds, the Docker images are not cached from build to build since you get a new machine for every build. This will make your builds on Microsoft-hosted agents run longer than those on your development machine.

* If you use Hosted Linux agents, then the agent itself runs in a container. This has some implications when you use docker-compose to spin up additional containers. As an example, there is no network connectivity from the agent container to the composition containers. Use `docker-compose exec` as a way of executing commands from the agent container in one of the composition containers.

::: moniker-end

* Check the version of Docker on the agent, and ensure that it matches what you have on your development machine. You can include a command line script `docker --version` in your build pipeline to print the version of Docker.
