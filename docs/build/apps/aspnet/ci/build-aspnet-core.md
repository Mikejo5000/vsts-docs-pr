---
title: Continuous integration for ASP.NET Core applications
description: Define a continuous integration (CI) build for your an ASP.NET Core app in Visual Studio Team Services or Microsoft Team Foundation Server (TFS)
ms.prod: vs-devops-alm
ms.technology: vs-devops-build
ms.assetid: 95ACB249-0598-4E82-B155-26881A5AA0AA
ms.manager: douge
ms.author: alewis
ms.date: 02/10/2017
---

# Build your ASP.NET Core app

[!INCLUDE [temp](../../../_shared/version.md)]

[ASP.NET Core](http://www.asp.net/core) is a lean and composable framework for building web and cloud applications. Here we'll show you how to define your continuous integration (CI) process.

## Get set up

For the instructions in this topic, you need an ASP.NET Core project in Visual Studio 2015 Update 3 or Visual Studio 2017.

> [!TIP]
> If you don't yet have an app but want to try this out, then see the [Q&A below](#new_solution).

## Define your CI build process

### Create the build definition

<ol>
    [!INCLUDE [include](../../../_shared/begin-create-build-definition.md)]

    <li>Start with an empty process.</li>


    <li>As the repository source, select the team project, repository, and branch.</li>

</ol>

### Add the tasks

Add the following tasks.

[!INCLUDE [include](../_shared/aspnet-core-build-steps.md)]

### Define variables

On the Variables tab, add the following variables:

|Name|Value|
|-|-|
|`BuildConfiguration`|`release`|
|`BuildPlatform`|`any cpu`|

### Enable continuous integration (CI)

On the Triggers tab, enable **continuous integration** (CI). This tells the system to queue a build whenever someone on your team commits or checks in new code.

[!INCLUDE [include](../_shared/aspnet-core-build-queue.md)]

## Queue and test the build

Save the build definition and queue a new build by selecting the **Queue new build** command.

Once the build is done (after a couple of minutes), click on the build number (such as "Build 332"), click the **Artifacts** tab, and then **Explore** to see the zip file produced by the build. This is the web deploy package that your release definition will consume to deploy your app.

[!INCLUDE [include](_shared/deploy-asp-web-app.md)]

## Q&A

<!-- BEGINSECTION class="md-qanda" -->

<h3 id="new_solution">How do I create an ASP.NET Core solution?</h3>

0. If you are using Visual Studio 2015 Update 3, then install [.NET Core 1.0.1 - VS 2015 Tooling Preview 2](https://www.microsoft.com/net/core#windows) or newer. If you are using Visual Studio 2017, then you're all set and can skip to the next step.

0. In Visual Studio, [connect to your team project](../../../../connect/connect-team-projects.md#visual-studio).

0. On the Team Explorer home page (Keyboard: Ctrl + 0, H), under **Solutions**, click **New**.

0. Select the **Visual C#** templates node, the **Web** sub-node.

0. Select **ASP.NET Core Web Application (.NET Core)** and click **OK**.

0. Select **Web Application** from the template list.

0. Click **Change Authentication**, select **No Authentication**, and click **OK**.

0. Clear **Host in the cloud** and click **OK**.

0. [Commit and push (Git)](../../../../git/share-your-code-in-git-vs.md) or [check in (TFVC)](../../../../tfvc/share-your-code-in-tfvc-vs.md) your code.

[!INCLUDE [temp](../../../_shared/qa-versions.md)]

<!-- BEGINSECTION class="md-qanda" -->
