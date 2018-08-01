---
title: Ruby
description: Building Ruby projects using VSTS and TFS
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: C517DBFB-EBCD-4CEA-B2BD-CE73B9DCA62C
ms.manager: douge
ms.author: alewis
author: andyjlewis
ms.reviewer: vijayma
ms.date: 08/01/2018
ms.topic: quickstart
monikerRange: 'vsts'
---

# Ruby

This guidance explains how to build Ruby projects.

> [!NOTE]
> To use YAML you must have the **Build YAML definitions** [preview feature](/vsts/project/navigation/preview-features) enabled on your organization.

## Example

> [!IMPORTANT]
> Complete the [YAML](../get-started-yaml.md) quickstart first before following these instructions.

If you want some sample code that works with this guidance, import (into VSTS or TFS) or fork (into GitHub) this repo:

```
https://github.com/adventworks/yuby-sample
```

<!-- TODO: Create the above repo with ruby sample -->

The sample code above includes a `.vsts-ci.yml` file at the root of the repository.
You can use this file to build the project. Push a trivial change to your YAML file and see how the build is triggered.
Then read through the rest of this topic learn some of the more common changes people make to customize the build process for their Ruby project.

<!-- TODO: Add a .vsts-ci.yml file to the above repository. -->

## Build environment

You can use VSTS to build your Ruby apps without needing to set up any infrastructure of your own.
The [Microsoft-hosted agents](../agents/hosted.md) in VSTS have Ruby pre-installed on them.
Use the **Hosted VS2017** agent queue (to build on Windows), the **Hosted Linux Preview** agent queue (to build on Linux), or the **Hosted macOS Preview** queue (to build on a MacOS).

The Microsoft hosted agents usually have the latest version of Ruby. See [Microsoft hosted agents](../agents/hosted.md) to know which version of Ruby is pre-installed.
If you need a different version, then you can use the `Use Ruby Version` task as part of your build process.

```yaml
steps:
- task: UseRubyVersion@0
  inputs:
    version: 2.1    // replace with the version that you desire
```

<!-- TODO: What about JRuby, etc? -->

> [!TIP]
> 
> You can also use [self-hosted agents](../agents/agents.md) to save additional time if you have a large repository or you run incremental builds.

## Manage dependencies

<!-- TODO: Fill in -->
<!-- TODO: Explain how users can use gem, gemfile, bundle, etc as part of their build script. -->
<!-- TODO: Talk about caching or the lack thereof -->

## Build and test your project

<!-- TODO: Fill in -->
<!-- TODO: Explain how to use rake as part of build script -->

## Package into a Docker container

<!-- TODO: Fill in -->
<!-- TODO: Explain the script to create a Docker container. Point to Docker.md for more details. Include a Dockerfile in the sample repo. -->
