---
title: Go
description: Building Go projects using VSTS and TFS
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: 9D728A05-F903-4F7E-968A-C59398192872
ms.manager: douge
ms.author: alewis
author: andyjlewis
ms.reviewer: vijayma
ms.date: 08/01/2018
ms.topic: quickstart
monikerRange: '>= tfs-2017'
---

# Go

::: moniker range="<= tfs-2018"
[!INCLUDE [temp](../_shared/concept-rename-note.md)]
::: moniker-end

This guidance explains how to build Go language projects.

::: moniker range="tfs-2017"

> [!NOTE]
> 
> This guidance applies to TFS version 2017.3 and newer.

::: moniker-end

::: moniker range="vsts"

> [!NOTE]
> To use YAML you must have the **Build YAML definitions** [preview feature](/vsts/project/navigation/preview-features) enabled on your organization.

::: moniker-end

## Example

If you want some sample code that works with this guidance, import (into VSTS or TFS) or fork (into GitHub) this repo:

```
https://github.com/adventworks/go-sample
```

# [YAML](#tab/yaml)

::: moniker range="vsts"

> [!IMPORTANT]
> If you are new to creating build pipelines using YAML, then complete the [YAML](../get-started-yaml.md) quickstart first before following these instructions.

The sample code above includes a `.vsts-ci.yml` file at the root of the repository.
You can use this file to build the project. Push a trivial change to your YAML file and see how the build is triggered.
Then read through the rest of this topic learn some of the more common changes people make to customize the build process for their Go project.

<!-- TODO: Add a .vsts-ci.yml file to the above repository. -->

::: moniker-end

::: moniker range="< vsts"
YAML builds are not yet available on TFS.
::: moniker-end

# [Designer](#tab/designer)

> [!IMPORTANT]
> If you are new to creating build pipelines, then complete the [designer](../get-started-designer.md) quickstart first before following these instructions.

After you have the sample code in your own repository, create a build pipeline and select the **Go** template. This automatically adds the tasks required to build the code in the sample repository.

Save the pipeline and queue a build to see it in action. Then read through the rest of this topic to learn some of the more common changes people make to customize the build process for their Go project.

---

## Build environment

::: moniker range="vsts"

You can use VSTS to build your Go apps without needing to set up any infrastructure of your own.
The [Microsoft-hosted agents](../agents/hosted.md) in VSTS have Go pre-installed on them.
Use the **Hosted VS2017** agent queue (to build on Windows), the **Hosted Linux Preview** agent queue (to build on Linux), or the **Hosted macOS Preview** queue (to build on a MacOS).

The Microsoft hosted agents usually have the latest version of Go. See [Microsoft hosted agents](../agents/hosted.md) to know which version of Go is pre-installed.
If you need a different version, then you can use the `Go tool installer` task as part of your build process.

<!-- TODO: Talk about how GOROOT and GOPATH are set. -->

# [YAML](#tab/yaml)

If you need a version of Go that is not already installed on the Microsoft-hosted agent, add the following snippet to your `.vsts-ci.yml` file:

```yaml
steps:
- task: GoTool@0
  inputs:
    version: 1.9    // replace with the version that you desire
```

# [Designer](#tab/designer)

If you need a version of Go that is not already installed on the Microsoft-hosted agent:

1. In the build pipeline, select **Tasks**, choose the phase that runs your build tasks, and then select **+** to add a new task to that phase.

1. In the task catalog, find and add the **Go Tool Installer** task.

1. Select the task and specify the version of the Go that you want to install.

---

> [!TIP]
> 
> You can also use [self-hosted agents](../agents/agents.md) to save additional time if you have a large repository or you run incremental builds.

::: moniker-end

::: moniker range="< vsts"
You can build your Go apps on a [self-hosted agent](../agents/agents.md#install).
Make sure that you have the necessary version of Go installed on the agent.
::: moniker-end

## Manage dependencies

<!-- TODO: Fill in -->
<!-- TODO: Explain how users can download dependencies as part of their CI. For instance, go get, godep restore, godeps.json, private dependencies, ??? -->

# [YAML](#tab/yaml)

::: moniker range="vsts"
<!-- TODO: Fill in -->
::: moniker-end

::: moniker range="< vsts"
YAML builds are not yet available on TFS.
::: moniker-end

# [Designer](#tab/designer)

<!-- TODO: Fill in -->

---

## Build and test your project

<!-- TODO: Fill in -->
<!-- TODO: Explain the script (and some flavors of it) to add in order to run a Go build -->

# [YAML](#tab/yaml)

::: moniker range="vsts"
<!-- TODO: Fill in -->
::: moniker-end

::: moniker range="< vsts"
YAML builds are not yet available on TFS.
::: moniker-end

# [Designer](#tab/designer)

<!-- TODO: Fill in -->

---

## Package into a Docker container

<!-- TODO: Fill in -->
<!-- TODO: Explain the script to create a Docker container. Point to Docker.md for more details. Include a Dockerfile in the sample repo. -->

# [YAML](#tab/yaml)

::: moniker range="vsts"
<!-- TODO: Fill in -->
::: moniker-end

::: moniker range="< vsts"
YAML builds are not yet available on TFS.
::: moniker-end

# [Designer](#tab/designer)

<!-- TODO: Fill in -->

---
