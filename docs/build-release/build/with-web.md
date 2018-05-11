---
title: CI build defined using the web
description: Define a continuous integration (CI) build using the web for a Visual Studio app in VSTS or Microsoft Team Foundation Server (TFS)
ms.prod: devops
ms.technology: devops-cicd
ms.topic: quickstart
ms.assetid: 513F0DDB-3F47-4D9B-9B57-73288AF22829
ms.manager: douge
ms.author: alewis
author: andyjlewis
ms.date: 5/10/2018
monikerRange: '>= tfs-2017'
---

# Use the web to create a CI pipeline

::: moniker range="vsts"
Visual Studio Team Services (VSTS) provides a highly customizable continuous integration (CI) process to automatically build your app whenever your team pushes or checks in code. 
::: moniker-end
::: moniker range="< vsts"
Team Foundation Server (TFS) provide a highly customizable continuous integration (CI) process to automatically build your app whenever your team pushes or checks in code. 
::: moniker-end
In this quickstart you learn how to define a CI process in your web browser. In this case it's for a Visual Studio solution with an ASP.NET 4 project.

## Prerequisites

::: moniker range="vsts"

[!INCLUDE [include](../_shared/ci-cd-prerequisites-vsts.md)]

::: moniker-end

::: moniker range="< vsts"

Make sure that you have [configured a build agent](../actions/agents/v2-windows.md) for your team project, and that you have a version of Visual Studio matching your development machine installed on the agent machine.

::: moniker-end

## Get the sample code

This quickstart works for apps targeting the .NET Framework 4 or newer. The sample app is a Visual Studio solution that has two projects: An ASP.NET Web Application project that targets .NET Framework 4.5.
::: moniker range="vsts"
The solution also has a Unit Test project, and in this tutorial we'll publish the results to VSTS.
::: moniker-end
::: moniker range="< vsts"
The solution also has a Unit Test project, and in this tutorial we'll publish the results to TFS.
::: moniker-end

[!INCLUDE [include](../apps/_shared/get-sample-code-intro.md)]

```
https://github.com/adventworks/aspnet4-sample
```

::: moniker range="vsts"

Where do you want to keep your code? Whichever service you choose, our system can automatically clone and pull code from it every time you push a change.

# [VSTS Git repo](#tab/gitvsts)

[!INCLUDE [include](../apps/_shared/get-sample-code-vsts-tfs-2017-update-2.md)]

# [GitHub repo](#tab/github)

[!INCLUDE [include](../apps/_shared/get-sample-code-github.md)]

---

::: moniker-end

[!INCLUDE [include](../apps/_shared/get-sample-code-other-repos-vsts-tfs.md)]

## Create the CI pipeline

[!INCLUDE [include](../_shared/ci-quickstart-intro.md)]

1. Create a new build definition.

 ::: moniker range="< vsts"

 Navigate to the **Files** tab of the **Code** hub, and then click **Set up build**.

 ![Screenshot showing button to set up build for a repository](../apps/_shared/_img/set-up-first-build-from-code-hub.png)

 You are taken to the **Build and Release** hub and asked to **Select a template** for the new build definition.
 
 ::: moniker-end

 ::: moniker range="vsts"

 # [VSTS Git repo](#tab/gitvsts)

 Navigate to the **Files** tab of the **Code** hub, and then click **Set up build**.

 ![Screenshot showing button to set up build for a repository](../apps/_shared/_img/set-up-first-build-from-code-hub.png)

 You are taken to the **Build and Release** hub and asked to **Select a template** for the new build definition.

 # [GitHub repo](#tab/github)

 Navigate to the **Builds** tab of the **Build and Release** hub in VSTS or TFS, and then click **+ New**. You are asked to **Select a template** for the new build definition.

   ---

  ::: moniker-end


1. In the right panel, click **ASP.NET**, and then click **Apply**.

 You now see all the tasks that were automatically added to the build definition by the template. These are the steps that will automatically run every time you push code changes.

1. For the **Agent queue**:

 ::: moniker range="vsts"

 * **VSTS:** Select _Hosted VS2017_. This is how you can use our pool of agents that have the software you need to build your app.
 
 ::: moniker-end

 ::: moniker range="< vsts"

 * **TFS:** Select a queue that includes a [Windows build agent](../actions/agents/v2-windows.md).
 
 ::: moniker-end

1. Click **Get sources** and then:

 ::: moniker range="< vsts"

 Observe that the new build definition is automatically linked to your repository.

 ::: moniker-end

 ::: moniker range="vsts"

 # [VSTS Git repo](#tab/gitvsts)

 Observe that the new build definition is automatically linked to your repository.

 # [GitHub repo](#tab/github)

 Select your version control repository. You'll need to authorize access to your repo.

 ::: moniker-end

 ---

1. Click the **Triggers** tab in the build definition. Enable the **Continuous Integration** trigger. This will ensure that the build process is automatically triggered every time you commit a change to your repository.

1. Click **Save & queue** to kick off your first build. On the **Save build definition and queue** dialog box, click **Save & queue**.

1. A new build is started. You'll see a link to the new build on the top of the page. Click the link to watch the new build as it happens.

[//]: # (TODO:> [!TIP])
[//]: # (TODO:> To learn more about GitHub CI builds, see [Define CI build process for your Git repo](#)

## View build summary

[!INCLUDE [include](../apps/_shared/view-build-summary.md)]

## Next steps

You've just learned the basics to create and run a CI build pipeline in your web browser.
This pipeline automatically builds and validates whatever code is checked in by your team. 
Now you're ready to learn how to configure your pipeline for the programming language you're using.

[//]: # (TODO: Add links to language topics)
