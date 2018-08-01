---
title: PHP
description: Building PHP projects using VSTS and TFS
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: D7475395-ECEA-448C-B925-1312AC7EE7A6
ms.manager: douge
ms.author: alewis
author: andyjlewis
ms.reviewer: vijayma
ms.date: 08/01/2018
ms.topic: quickstart
monikerRange: 'vsts'
---

# PHP

This guidance explains how to build PHP projects.

> [!NOTE]
> To use YAML you must have the **Build YAML definitions** [preview feature](/vsts/project/navigation/preview-features) enabled on your organization.

## Example

> [!IMPORTANT]
> Complete the [YAML](../get-started-yaml.md) quickstart first before following these instructions.

If you want some sample code that works with this guidance, import (into VSTS or TFS) or fork (into GitHub) this repo:

```
https://github.com/adventworks/php-sample
```

The sample code above includes a `.vsts-ci.yml` file at the root of the repository.
You can use this file to build the project. Push a trivial change to your YAML file and see how the build is triggered.
Then read through the rest of this topic learn some of the more common changes people make to customize the build process for their PHP project.

<!-- TODO: Add a .vsts-ci.yml file to the above repository. -->

## Build environment

You can use VSTS to build your PHP projects without needing to set up any infrastructure of your own.
The [Microsoft-hosted agents](../agents/hosted.md) in VSTS have PHP pre-installed on them.
Use the **Hosted VS2017** agent queue (to build on Windows), the **Hosted Linux Preview** agent queue (to build on Linux), or the **Hosted macOS Preview** queue (to build on a MacOS).

The Microsoft hosted agents usually have the latest version of PHP. See [Microsoft hosted agents](../agents/hosted.md) to know which version of PHP is pre-installed.
If you need a different version, then
<!-- TODO: Talk about how to get another version of PHP on hosted agents. -->

> [!TIP]
> 
> You can also use [self-hosted agents](../agents/agents.md) to save additional time if you have a large repository or you run incremental builds.

## Manage dependencies

<!-- TODO: Fill in -->
<!-- TODO: Explain how users can download dependencies as part of their CI. -->

## Build and test your project

<!-- TODO: Fill in -->
<!-- TODO: Explain the script (and some flavors of it) to add in order to run a PHP build, for example composer, phpunit -->

## Package into a Docker container

<!-- TODO: Fill in -->
<!-- TODO: Explain the script to create a Docker container. Point to Docker.md for more details. Include a Dockerfile in the sample repo. -->
