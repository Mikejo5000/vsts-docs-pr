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

[//]: # (TODO: screenshot to set context)

Now you'll modify a YAML file that has a well-known name. The first time you change this file, VSTS automatically uses it to create your build defniition. For this example, to learn some of the basics, you'll change the YAML file to use tasks instead of a script. 

1. Navigate to the **Code** hub, choose the **Files** tab, and then choose the repository you created in the above steps.

1. Choose the **.vsts-ci.yml** file, and then click **Edit**.

1. Replace the contents of the file with the following:

 ```YAML
steps:

- task: dotNetCoreCLI@1
  inputs:
    command: restore
    projects: "**/*.csproj"
  displayName: dotnet restore

- task: dotNetCoreCLI@1
  inputs:
    command: build
    projects: "**/*.csproj"
    arguments: --configuration release
  displayName: dotnet build

- task: dotNetCoreCLI@1
  inputs:
    command: test 
    projects: "**/*Tests/*.csproj"
    arguments: --configuration release
  displayName: dotnet build

- task: dotNetCoreCLI@1
  inputs:
    command: publish
    arguments: --configuration release --output $(build.artifactstagingdirectory)
  displayName: dotnet publish

- task: publishBuildArtifacts@1
  inputs:
    PathtoPublish: $(Build.ArtifactStagingDirectory)
    ArtifactName: drop
    ArtifactType: Container
```

1. Commit your change to the master branch.

1. Navigate to the **Build and Release** hub.

1. Observe that there's a new build named _{name-of-your-repo}_ YAML CI. A build is queued; it's status could be either not started or running. Click the number of the build: _{year}{month}{day}.1_.

1. In the left column of the running build, click **Job**. After a hosted agent is assigned to your job and the agent is initialized, then you'll see information about the build in the console.

The changes you just made affect how the build looks. Each step shows up in the build summary instead of as the output from a single script.

[//]: # (TODO: SCREENSHOT)

> In this case, these changes also change what the build does. For example, the `dotnet restore` command that is run by the script in the repo creates .DLL files, but doesn't create a .ZIP file. After you've completed the above steps, you're using the `dotNetCoreCLI` task, which in addition to creating the .DLL file, also creates a web deployment package (a .ZIP file) that is more efficient to deploy.

## Next steps

[//]: # (TODO: sort out apps/_shared/ci-web-app-next-steps* and implement here)

You've just put your own CI build process in place to automatically build and validate whatever code is checked in by your team.

[//]: # (TODO: if we don't publish how-to below, I guess we should link to GitHub docs; but that might feel a bit of a stark dropoff, so I guess we have to publish the How To with at least minimal context, which can then link to GitHub docs)
[//]: # (TODO: > [!div class="nextstepaction"])
[//]: # (TODO: > [Learn more about YAML builds](build-yaml.md)

### Deploy your app

If you want to deploy to:

* **Azure web app or to an IIS server**: You're already good to go after following the above steps. Your CI build is publishing a .ZIP file. See either
 - [Deploy to Azure Web App](../apps/cd/deploy-webdeploy-webapps.md)
 - [Deploy to a Windows VM](../apps/cd/deploy-webdeploy-iis-deploygroups.md)

* **Linux VM**: 

[//]: # (TODO: finish)


| If you want to deploy to a... | Then publish your artifact as a...|
|-|-|
| Azure web app or to an IIS server | .ZIP file. In this case you're already good to go after following the above steps. Next step is one of the following: <ul><li>[Deploy to Azure Web App](../apps/cd/deploy-webdeploy-webapps.md)</li><li>[Deploy to a Windows VM](../apps/cd/deploy-webdeploy-iis-deploygroups.md)</li></ul> | 
| Linux VM | Simple folder. To do this, remove the **Archive files** task from your build definition. |
| Container service (such as Azure web apps for containers, or a Kubernetes cluster) | Container. Next step: [Build and push a container for your app](../apps/containers/build.md).|


### Enhance your Git workflows

Now that you have a CI build process for your master branch, you can extend the process to work with other branches in your repository, or to validate all pull requests. See:

* [CI builds for Git in VSTS](../actions/ci-build-git.md)

* [CI builds for GitHub](../actions/ci-build-github.md)
