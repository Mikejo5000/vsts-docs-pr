---
title: CI build for a Node.js app with Gulp
description: Define a continuous integration (CI) build process for your Node.js app with Gulp in VSTS or Team Foundation Server
ms.prod: vs-devops-alm
ms.technology: vs-devops-build
ms.topic: get-started-article
ms.assetid: F0829366-2AC1-4344-9494-98CACEC38806
ms.manager: douge
ms.author: alewis
ms.date: 08/28/2017
---

# Build your Node.js app with Gulp

Follow these steps to quickly set up a CI process for your Node.js app using VSTS. The sample app we use here is a Node server that echoes "Hello world". Tests for the app are written using mocha framework. A gulp file is used to run the tests and to convert the results into junit format so that they can be published to VSTS or TFS.

## Prerequisites

[!INCLUDE [include](../../_shared/ci-cd-prerequisites-vsts.md)]

## Get sample app code

[!INCLUDE [include](../_shared/get-sample-code-intro.md)]

```
https://github.com/adventworks/nodejs-sample
```

Choose your version control system for specific instructions:

# [VSTS Git](#tab/vstsgit)

[!INCLUDE [include](../_shared/get-sample-code-vsts-tfs-2017-update-2.md)]

# [GitHub](#tab/github)

[!INCLUDE [include](../_shared/get-sample-code-github.md)]

---

[!INCLUDE [include](../_shared/get-sample-code-other-repos-vsts.md)]

## Set up CI - build process

The simplest way to define your build process is in a **.vsts-ci.yml** file and to check in that file at the root of your repository. The advantage of this approach is that your build process is managed as code and it follows the same branch structure as the rest of your application code.

Another way to define your build process is to use the build definition editor in VSTS. This provides a more visual approach of your process.

# [YAML](#tab/yaml/vstsgit)

The sample app already has the .vsts-ci.yml file. View this file in your version control repository and notice the steps for building, archiving, and publishing the app.

# [YAML](#tab/yaml/github)

1. Navigate to the **Builds** tab of the **Build and Release** hub in VSTS or TFS, and then click **+ New**. You are asked to **Select a template** for the new build definition.

1. In the right panel, select **YAML** and click **Apply**.

1. For the **Default agent queue**, select _Hosted VS2017_. This is how you can use our pool of agents that have the software you need to build your app.

1. For the **Yaml path**, enter **.vsts-ci.yml**.

1. Click **Get sources**. Select your version control repository. You'll need to authorize access to your repo.

# [Editor](#tab/editor/vstsgit)

1. Navigate to the **Files** tab of the **Code** hub, and then click **Set up build**.

  ![Screenshot showing button to set up build for a repository](../_shared/_img/set-up-first-build-from-code-hub.png)

  You are taken to the **Build & Release** hub and asked to **Select a template** for the new build definition.

1. In the right panel, search for `node`, select **NodeJS with Gulp**, and then click **Apply**.

  ![apply node.js gulp template](_img/apply-nodejs-gulp-template.png)

  You now see all the tasks that were automatically added to the build definition by the template. These are the steps that will automatically run every time you check in code.

1. For the **Default agent queue**, select _Hosted VS2017_. This is how you can use our pool of agents that have the software you need to build your app.

1. Select the **Run gulp** task from the tasks. On the right side, you see the parameters for the task. Under the section JUnit Test Results, select the option to Publish to TFS/VSTS.

1. Click the **Triggers** tab in the build definition. Enable the **Continuous Integration** trigger. This will ensure that the build process is automatically triggered every time you commit a change to your repository.

# [Editor](#tab/editor/github)

1. Navigate to the **Builds** tab of the **Build and Release** hub in VSTS or TFS, and then click **+ New**. You are asked to **Select a template** for the new build definition.

1. In the right panel, search for `node`, select **NodeJS with Gulp**, and then click **Apply**.

  ![apply node.js gulp template](_img/apply-nodejs-gulp-template.png)

  You now see all the tasks that were automatically added to the build definition by the template. These are the steps that will automatically run every time you check in code.

1. For the **Default agent queue**, select _Hosted VS2017_. This is how you can use our pool of agents that have the software you need to build your app.

1. Click **Get sources**. Select your version control repository. You'll need to authorize access to your repo.

1. Select the **Run gulp** task from the tasks. On the right side, you see the parameters for the task. Under the section JUnit Test Results, select the option to Publish to TFS/VSTS.

1. Click the **Triggers** tab in the build definition. Enable the **Continuous Integration** trigger. This will ensure that the build process is automatically triggered every time you commit a change to your repository.

---

## Set up CI - build environment (Optional)

If you followed the steps above, your build will run on a machine managed by Microsoft in the Hosted VS2017 pool. You can choose to run the build in your custom Docker container if you use containers in your development environment, or on your own private agent if you have special prerequisites that are not met on the hosted agents.

# [Hosted pool](#tab/hosted)

No additional steps are necessary to run your build on the hosted pool.

# [Container](#tab/container/yaml)

Edit the **.vsts-ci.yml** file in the master branch of your repository by adding the following line at the beginning:

```
_PREVIEW_DOCKER_CONTAINER_ = adventworks/nodejs-build-env
```

# [Container](#tab/container/editor)

* Select the **Variables** tab in your build definition, and add the following variable:

```
_PREVIEW_DOCKER_CONTAINER_ = adventworks/nodejs-build-env
```

This defines a sample Node build environment that we have uploaded to the public Docker container registry.

---

## Make a change

1. Click **Save and queue** to kick off your first build. On the **Queue build** dialog box, click **Queue**.

1. A new build is started. You'll see a link to the new build on the top of the page. Click the link to watch the new build as it happens.


[//]: # (TODO:> [!TIP])
[//]: # (TODO:> To learn more about GitHub CI builds, see [Define CI build process for your Git repo](#)

## View the build summary

[!INCLUDE [include](../_shared/view-build-summary.md)]

## Next steps

[!INCLUDE [include](../_shared/ci-web-app-next-steps.md)]
