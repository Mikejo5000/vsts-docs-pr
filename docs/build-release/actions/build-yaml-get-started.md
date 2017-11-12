---
title: Get started with a CI Build in code using YAML
description: Get started defining your CI build process in YAML in Visual Studio Team Services (VSTS) and Team Foundation Server (TFS)
ms.prod: vs-devops-alm
ms.technology: vs-devops-build
ms.assetid: 70DE052F-9F5F-4733-B831-EF8C2C490716
ms.manager: douge
ms.author: alewis
ms.date: 11/11/2017
---

# Get started with configuring your CI Build in code using YAML

**VSTS**

When you define a CI build on VSTS, you've got a fundamental choice: use a web-based interface or configure your CI process as code in a YAML build. Here we'll take you on a quick walkthrough so you can try a YAML build and see how it works.

## Prerequisites

[!INCLUDE [include](../_shared/ci-cd-prerequisites-vsts.md)]

[!INCLUDE [include](../_shared/ci-cd-prerequisites-tfs.md)]

## Get the sample code

[!INCLUDE [include](../apps/_shared/get-sample-code-intro.md)]

```
https://github.com/adventworks/dotnetcore-sample
```

Next, choose which kind of Git service you're using:

# [VSTS or TFS repo](#tab/vsts)

[!INCLUDE [include](../apps/_shared/get-sample-code-vsts-tfs-2017-update-2.md)]

# [GitHub repo](#tab/github)

[!INCLUDE [include](../apps/_shared/get-sample-code-github.md)]

---

[!INCLUDE [include](../apps/_shared/get-sample-code-other-repos-vsts.md)]

## Set up continuous integration

[!INCLUDE [include](../_shared/ci-quickstart-intro.md)]

## Next steps

[//]: # (TODO: sort out apps/_shared/ci-web-app-next-steps* and implement here)

You've just put your own CI build process in place to automatically build and validate whatever code is checked in by your team.

> [!div class="nextstepaction"]
> [Learn more about YAML builds](build-yaml.md)

### Deploy your app

If you want to deploy to:

* **Azure web app or to an IIS server**: You're already good to go after following the above steps. Your CI build is publishing a .ZIP file. See either
 - [Deploy to Azure Web App](../apps/cd/deploy-webdeploy-webapps.md)
 - [Deploy to a Windows VM](../apps/cd/deploy-webdeploy-iis-deploygroups.md)

* **Linux VM**: 
Remove 

| If you want to deploy to a... | Then publish your artifact as a...|
|-|-|
| Azure web app or to an IIS server | .ZIP file. In this case you're already good to go after following the above steps. Next step is one of the following: <ul><li>[Deploy to Azure Web App](../apps/cd/deploy-webdeploy-webapps.md)</li><li>[Deploy to a Windows VM](../apps/cd/deploy-webdeploy-iis-deploygroups.md)</li></ul> | 
| Linux VM | Simple folder. To do this, remove the **Archive files** task from your build definition. |
| Container service (such as Azure web apps for containers, or a Kubernetes cluster) | Container. Next step: [Build and push a container for your app](../apps/containers/build.md).|


### Enhance your Git workflows

Now that you have a CI build process for your master branch, you can extend the process to work with other branches in your repository, or to validate all pull requests. See:

* [CI builds for Git in VSTS](../actions/ci-build-git.md)

* [CI builds for GitHub](../actions/ci-build-github.md)
