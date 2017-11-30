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

# Get started configuring your CI Build in code using YAML

**VSTS**

When you define a CI build on VSTS, you've got a fundamental choice: use a web-based interface or configure your CI process as code in a YAML build. Here we'll take you on a quick walkthrough so you can try a YAML build and see how it works.

In this tutorial, you'll learn how to:

> [!div class="checklist"]
> * Get the sample code
> * Set up continuous integration (CI)

## Prerequisites

> [!NOTE]
> To use this capability, you must have the **Build YAML definitions** [preview feature](/vsts/collaborate/preview-features) enabled on your account.

[!INCLUDE [include](../_shared/ci-cd-prerequisites-vsts.md)]

[!INCLUDE [include](../_shared/ci-cd-prerequisites-tfs.md)]

## Get the sample code

[!INCLUDE [include](../apps/_shared/get-sample-code-intro.md)]

# [ASP.NET Core](#tab/aspnet-core)

```
https://github.com/adventworks/dotnetcore-sample
```

# [Node.js](#tab/node-js)

```
https://github.com/adventworks/nodejs-sample
```

---

Next, choose which kind of Git service you're using:

# [VSTS or TFS repo](#tab/vsts)

[!INCLUDE [include](../apps/_shared/get-sample-code-vsts-tfs-2017-update-2.md)]

# [GitHub repo](#tab/github)

[!INCLUDE [include](../apps/_shared/get-sample-code-github.md)]

---

## Set up continuous integration

[!INCLUDE [include](../_shared/ci-quickstart-intro.md)]

# [VSTS or TFS repo](#tab/vsts/aspnet-core)

To create a definition that is configured as code, you'll modify a YAML file in the repo root that has a well-known name: **.vsts-ci.yml**. The first time you change this file, VSTS automatically uses it to create your build definition.

1. Navigate to the **Code** hub, choose the **Files** tab, and then choose the repository you created in the above steps.

2. Choose the **.vsts-ci.yml** file, and then click **Edit**.

3. Replace the contents of the file with the following:

   [!code-yaml[code](_shared/yaml-build-definition-aspnet-core.md)]

4. Commit your change to the master branch.

5. Navigate to the **Build and Release** hub.

6. Observe that there's a new build definitionnamed _{name-of-your-repo} YAML CI_. A build is queued; its status could be either not started or running. Click the number of the build: _{year}{month}{day}.1_.

7. In the left column of the running build, click **Job**. After a hosted agent is assigned to your job and the agent is initialized, then you'll see information about the build in the console.

For this example, to learn some of the basics, you changed the YAML file to use the  `dotNetCoreCLI` task instead of calling the `dotnet` command directly in a script. The changes you made affect how the build output is organized. Each step is shown and can be inspected in the build summary, instead of all the output combined in one log from a single script.

The changes you made also modified what the build does. For example, the `dotnet restore` command you replaced creates .DLL files, but it doesn't create a web deployment file. After you've completed the above steps, your build instead uses the `dotNetCoreCLI` task, which in addition to creating the .DLL file, also creates a web deployment package (a .ZIP file) that is more efficient to deploy.

# [VSTS or TFS repo](#tab/vsts/node-js)

To create a definition that is configured as code, you'll modify a YAML file in the repo root that has a well-known name: **.vsts-ci.yml**. The first time you change this file, VSTS automatically uses it to create your build definition.

1. Navigate to the **Code** hub, choose the **Files** tab, and then choose the repository you created in the above steps.

2. Choose the **.vsts-ci.yml** file, and then click **Edit**.

3. Replace the contents of the file with the following:

   [!code-yaml[code](_shared/yaml-build-definition-node-js.md)]

4. Commit your change to the master branch.

5. Navigate to the **Build and Release** hub.

6. Observe that there's a new build definitionnamed _{name-of-your-repo} YAML CI_. A build is queued; its status could be either not started or running. Click the number of the build: _{year}{month}{day}.1_.

7. In the left column of the running build, click **Job**. After a hosted agent is assigned to your job and the agent is initialized, then you'll see information about the build in the console.

# [GitHub repo](#tab/github/aspnet-core)

In GitHub:

1. Edit the **.vsts-ci.yml** file in the root of your repo, and replace the contents of the file with the following:

   [!code-yaml[code](_shared/yaml-build-definition-aspnet-core.md)]

1. Commit your change to the master branch.

In VSTS:

1. Navigate to the **Builds** tab of the **Build and Release** hub, and then click **+ New**. You are asked to **Select a template** for the new build definition.

1. Select **YAML**, and then select **Apply**.

1. Select **Get sources**, and then select your version control repository. You'll need to authorize access to your repo.

1. Select **Process**.

1. For the **Agent queue** select _Hosted VS2017_. This is how you can use our pool of agents that have the software you need to build your app.

1. For the **Yaml path**, select the **.vsts-ci.yml** file in the root of your repo.

1. Select the **Triggers** tab, and then enable continuous integration (CI).

1. Save and queue the build, and then click the number of the build: _{year}{month}{day}.1_ that has been queued.

1. In the left column of the running build, click **Job**. After a hosted agent is assigned to your job and the agent is initialized, then you'll see information about the build in the console.

# [GitHub repo](#tab/github/node-js)

In GitHub:

1. Edit the **.vsts-ci.yml** file in the root of your repo, and replace the contents of the file with the following:

   [!code-yaml[code](_shared/yaml-build-definition-aspnet-core.md)]

1. Commit your change to the master branch.

In VSTS:

1. Navigate to the **Builds** tab of the **Build and Release** hub, and then click **+ New**. You are asked to **Select a template** for the new build definition.

1. Select **YAML**, and then select **Apply**.

1. Select **Get sources**, and then select your version control repository. You'll need to authorize access to your repo.

1. Select **Process**.

1. For the **Agent queue** select _Hosted VS2017_. This is how you can use our pool of agents that have the software you need to build your app.

1. For the **Yaml path**, select the **.vsts-ci.yml** file in the root of your repo.

1. Select the **Triggers** tab, and then enable continuous integration (CI).

1. Save and queue the build, and then click the number of the build: _{year}{month}{day}.1_ that has been queued.

1. In the left column of the running build, click **Job**. After a hosted agent is assigned to your job and the agent is initialized, then you'll see information about the build in the console.

---

## Next steps

You've just put your own CI build process in place with the configuration as code that automatically builds and validates your app whenever you change either your app or your build process. Your next step depends on what you want to do.

### Deploy your app


# [ASP.NET Core](#tab/aspnet-core)

| If you want to deploy to a... | Then publish your artifact as a...|
|-|-|
| Azure web app or to an IIS server | .ZIP file. In this case you're already good to go after following the above steps. Next step is one of the following: <ul><li>[Deploy to Azure Web App](../apps/cd/deploy-webdeploy-webapps.md)</li><li>[Deploy to a Windows VM](../apps/cd/deploy-webdeploy-iis-deploygroups.md)</li></ul> | 
| Linux VM | Simple folder. To do this, in the **.vsts-ci.yml** file, set `zipAfterPublish` to `false`, and then see [Deploy to a Linux Virtual Machine](../apps/cd/deploy-linuxvm-deploygroups.md)|

# [Node.js](#tab/node-js)

| If you want to deploy to a... | Then publish your artifact as a...|
|-|-|
| Azure web app or to an IIS server | .ZIP file. In this case you're already good to go after following the above steps. Next step is one of the following: <ul><li>[Deploy to Azure Web App](../apps/cd/deploy-webdeploy-webapps.md)</li><li>[Deploy to a Windows VM](../apps/cd/deploy-webdeploy-iis-deploygroups.md)</li></ul> | 
| Linux VM | Simple folder. To do this, change the content of to the **.vsts-ci.yml** file to the following, and then see [Deploy to a Linux Virtual Machine](../apps/cd/deploy-linuxvm-deploygroups.md)|

```yaml
steps:
- task: Npm@1
  displayName: npm install

- task: Gulp@0
  inputs:
    publishJUnitResults: "true"
    displayName: Gulp

- task: PublishBuildArtifacts@1
  inputs:
    PathtoPublish: $(Build.SourcesDirectory)
    ArtifactName: "drop"
    ArtifactType: "Container"
    displayName: Publish the artifacts
```

---

### Learn more about YAML builds

Learn more about the advantages and how to use YAML builds.

> [!div class="nextstepaction"]
> [Learn more about YAML builds](build-yaml.md)

### Enhance your Git workflows

Now that you have a CI build process for your master branch, you can extend the process to work with other branches in your repository, or to validate pull requests. 

# [VSTS or TFS repo](#tab/vsts)

> [!div class="nextstepaction"]
> [CI builds for Git in VSTS](../actions/ci-build-git.md)

# [GitHub repo](#tab/github)

> [!div class="nextstepaction"]
> [CI builds for GitHub](../actions/ci-build-github.md)

---