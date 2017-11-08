---
title: CI build for a Docker-enabled app
description: Define a continuous integration (CI) build process for your Docker-enabled app in VSTS or Microsoft Team Foundation Server (TFS)
ms.prod: vs-devops-alm
ms.technology: vs-devops-build
ms.assetid: E5BEDC1D-0209-40F3-A2AB-591CB7AE97E8
ms.manager: douge
ms.author: alewis
ms.date: 09/27/2017
---

# Build and push a container for your app

In this quickstart you learn how to define CI process for your Docker-enabled application using VSTS. The CI process will publish a new container image to Azure Container Registry every time a change is pushed to the application code.

## Prerequisites

* A working CI set up for your application using VSTS. Follow the steps in [Build your Node.js app with Gulp](../nodejs/build-gulp.md) or [Build your ASP.NET Core app](../aspnet/build-aspnet-core.md).

* An Azure subscription. If you don't have one, you can [create one for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

[!INCLUDE [create-azure-container-registry](../_shared/create-azure-container-registry.md)]

## Modify the build definition

If you created a build definition using one of the topics described in pre-requisites, your build would produce a zip archive by default. This is convenient if you plan to deploy the app to an Azure web app or to an IIS server. If your goal is to deploy the app to Azure web apps for containers or a Kubernetes cluster, then you must publish the app as a container.

<!--
The steps for doing this depend on whether your CI process is defined through a YAML file or through the web editor in VSTS.

# [Editor](#tab/editor)
-->

1. Remove the **Archive files** task and the **Publish artifacts** task from the build definition.

1. Select **+ Add Task** to add another task to the build definition. From the displayed task catalog, select **Docker** task. Change the parameters for this task as follows:

   * **Azure subscription:** Select a connection from the list under **Available Azure Service Connections** or create a more restricted permissions connection to your Azure subscription. If you are using VSTS and if you see an **Authorize** button next to the input, click on it to authorize VSTS to connect to your Azure subscription. If you are using TFS or if you do not see
     the desired Azure subscription in the list of subscriptions, see [Azure Resource Manager service endpoint](../../concepts/library/service-endpoints.md#sep-azure-rm) to manually set up the connection.

   * **Azure Container Registry:** Select the Azure container registry that you created above.

   * **Action:** Build an image.

1. Select **+ Add Task** to add another **Docker** task to the build definition.
   Make sure that the task is inserted _after_ the previous **Docker** task. Change the parameters for this task as follows:

   * **Azure subscription:** Same as in previous task.

   * **Azure Container Registry:** Same as in previous task.

   * **Action:** Push an image.

1. Click **Save and queue** to kick off a build. On the **Queue build** dialog box, click **Queue**.

1. A new build is started. You'll see a link to the new build on the top of the page. Click the link to watch the new build as it happens. Verify that a Docker container image is built and pushed to the Azure container registry.

<!--
# [Container](#tab/yaml)

This is not yet supported in YAML.
---
-->
