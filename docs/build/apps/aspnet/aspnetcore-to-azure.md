---
title: Build and deploy your ASP.NET Core app to Azure
description: Define a continuous integration (CI) build for your an ASP.NET Core app in Visual Studio Team Services or Microsoft Team Foundation Server (TFS)
ms.prod: vs-devops-alm
ms.technology: vs-devops-build
ms.assetid: B5F1C4D4-6A3D-48A0-9D88-3E1B7BF5D152
ms.manager: douge
ms.author: alewis
ms.date: 02/10/2017
---

# Build and deploy your ASP.NET Core app to Azure

[!INCLUDE [temp](../../_shared/version.md)]

[!INCLUDE [temp](../../_shared/ci-cd-newbies.md)]

[ASP.NET Core](http://www.asp.net/core) is a lean and composable framework for building web and cloud applications. Here we'll show you how to create a continuous integration (CI) and continuous deployment (CD) pipeline to automatically build and deploy your ASP.NET Core app to [Azure](https://azure.microsoft.com/).

In this walkthrough, we'll show how to build a release pipeline in Visual Studio Team Services for an ASP.NET Core web application project.

> [!TIP]
> If you don't yet have an app but want to try this out, then see the [Q&A below](#new_solution).

[!INCLUDE [temp](_shared/steps.md)]

[!INCLUDE [temp](_shared/setup.md)]

[!INCLUDE [include](../_shared/azure-web-app-setup.md)]

[!INCLUDE [temp](_shared/define-ci-build.md)]

### Create the build definition

In this section we'll create a build definition for the ASP.NET Core web application, starting with an empty definition and adding each step manually. The result will be a .ZIP file for the web application that's stored where it can be accessed by the release definition we'll create in the next section.

<ol>
    [!INCLUDE [include](../../_shared/begin-create-build-definition.md)]

    <li>Start wtih an **empty** process.</li>

    <li>As the repository source, select the team project, repository, and branch.</li>

</ol>

### Add the tasks

Add the following tasks.

> [!Tip]
>
> In the left-hand column of this table, the name of the step indicates the category and step names as they appear in the Task Catalog dialog box. You can also add all the steps without closing the dialog box, and then fill in the details on the right-hand column. Values in the form of `$(name)` are *variables* that we'll define shortly.

[!INCLUDE [include](_shared/aspnet-core-build-steps.md)]

### Define variables

[Variables](../../define/variables.md) give you a convenient way to get key bits of data into various parts of your build process. You refer to a variable using `$(<variable_name>)`. Some variables are pre-defined; others you need to define directly.

On the Variables tab, add the following variables:

|Name|Value|
|-|-|
|`BuildConfiguration`|`release`|
|`BuildPlatform`|`any cpu`|

[!INCLUDE [include](_shared/aspnet-core-build-queue.md)]

### Enable continuous integration (CI)

On the Triggers tab, enable **continuous integration** (CI). This tells the system to queue a build whenever someone on your team commits or checks in new code.

### Queue and test the build

Save the build definition and queue a new build by selecting the **Queue new build** command.

Once the build is done (after a couple of minutes), click on the build number (such as "Build 332"), click the **Artifacts** tab, and then **Explore** to see the zip file produced by the build. This is the web deploy package that your release definition will consume to deploy your app.

After you've run the build, you're ready to create a release definition to deploy your app to Azure.

[!INCLUDE [include](../_shared/create-release.md)]

[!INCLUDE [include](_shared/commit-build-release.md)]

## Q&A

<!-- BEGINSECTION class="md-qanda" -->

<h3 id="new_solution">How do I create an ASP.NET Core solution?</h3>

1. If you are using Visual Studio 2015 Update 3, then install [.NET Core 1.0.1 - VS 2015 Tooling Preview 2](https://www.microsoft.com/net/core#windows) or newer. If you are using Visual Studio 2017, then you're all set and can skip to the next step.

1. In Visual Studio, [connect to your team project](../../../connect/connect-team-projects.md#visual-studio).

1. On the Team Explorer home page (Keyboard: Ctrl + 0, H), under **Solutions**, click **New**.

1. Select the **Visual C#** templates node, the **Web** sub-node.

1. Select **ASP.NET Core Web Application (.NET Core)** and click **OK**.

1. Select **Web Application** from the template list.

1. Click **Change Authentication**, select **No Authentication**, and click **OK**.

1. Clear **Host in the cloud** and click **OK**.

1. [Commit and push (Git)](../../../git/share-your-code-in-git-vs.md) or [check in (TFVC)](../../../tfvc/share-your-code-in-tfvc-vs.md) your code.

[!INCLUDE [temp](../../_shared/qa-versions.md)]

<!-- BEGINSECTION class="md-qanda" -->
