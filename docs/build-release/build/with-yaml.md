---
title: CI build defined using YAML
description: Define a continuous integration (CI) build process for your Node.js app with Gulp in VSTS
ms.prod: devops
ms.technology: devops-cicd
ms.topic: quickstart
ms.assetid: 5A8F1A12-72BF-4985-9B27-65CBC08462F7
ms.manager: douge
ms.author: alewis
author: andyjlewis
ms.date: 5/10/2018
monikerRange: 'vsts'
---

# Use YAML to create a CI pipeline

Visual Studio Team Services (VSTS) provides a highly customizable continuous integration (CI) process to automatically build your app whenever your team pushes or checks in code. 
In this quickstart you learn how to define a CI process using YAML for a JavaScript app, in this case an Node.js Gulp app.

## Prerequisites

[!INCLUDE [include](../_shared/ci-cd-prerequisites-vsts.md)]

## Get the sample code

The sample app we use here is a Node server that echoes "Hello world". Tests for the app are written using mocha framework. 
A gulp file is used to run the tests and to convert the results into junit format so that they can be published to VSTS.

[!INCLUDE [include](../apps/_shared/get-sample-code-intro.md)]

```
https://github.com/adventworks/nodejs-sample
```

Where do you want to keep your code? Whichever service you choose, our system can automatically clone and pull code from it every time you push a change.

# [VSTS Git repo](#tab/gitvsts)

[!INCLUDE [include](../apps/_shared/get-sample-code-vsts.md)]

# [GitHub repo](#tab/github)

[!INCLUDE [include](../apps/_shared/get-sample-code-github.md)]

---

[!INCLUDE [include](../apps/_shared/get-sample-code-other-repos-vsts.md)]

## Create the CI pipeline

[!INCLUDE [include](../_shared/ci-quickstart-intro.md)]

Begin by creating your build definition.

# [VSTS Git repo](#tab/gitvsts)

To create a definition that is configured as code, you'll modify a YAML file in the repo root that has a well-known name: **.vsts-ci.yml**. The first time you change this file, VSTS automatically uses it to create your build definition.

1. Navigate to the **Code** hub, choose the **Files** tab, and then choose the repository you created in the above steps.

1. Choose the **.vsts-ci.yml** file, and then choose **Edit**.

1. Replace the contents of the file with code below.

# [GitHub repo](#tab/github)

To create a definition that is configured as code, you'll modify a YAML file in the repo root that has a well-known name: **.vsts-ci.yml**. You'll then create a build definition that points to the YAML file.

In GitHub:

1. Edit the **.vsts-ci.yml** file in the root of your repo, and replace the contents of the file with code below.

---

```yaml
steps:

- task: Npm@1
  displayName: npm install

- task: Gulp@0
  inputs:
    publishJUnitResults: "true"
  displayName: Gulp

- task: ArchiveFiles@1
  inputs:
    rootFolder: "$(System.DefaultWorkingDirectory)"
    includeRootFolder: "false"
  displayName: Zip up the files

- task: PublishBuildArtifacts@1
  inputs:
    PathtoPublish: $(Build.ArtifactStagingDirectory)
    ArtifactName: "drop"
    ArtifactType: "Container"
  displayName: Publish the artifacts
```

Commit the above change to the master branch.

## Finish the CI process definition

You're nearly ready to go. Just a few more steps to complete your CI build process.

# [VSTS or TFS repo](#tab/gitvsts)

1. Navigate to the **Build and Release** hub.

1. Observe that there's a new build definition named _{name-of-your-repo} YAML CI_. A build is queued; its status could be either not started or running. Choose the number of the build: _{year}{month}{day}.1_.

1. In the left column of the running build, select **Job**. After an agent is assigned to your job and the agent is initialized, then you'll see information about the build in the console.

# [GitHub repo](#tab/github)

In VSTS:

1. Navigate to the **Builds** tab of the **Build and Release** hub, and then choose **+ New**. You're asked to **Select a template** for the new build definition.

1. Select **YAML**, and then select **Apply**.

1. Select **Get sources**, select **GitHub**, and then select your version control repository. You'll need to authorize access to your repo.

1. Select **Process**.

1. For the **Agent queue** select _Hosted Linux_. This is how you can use our pool of agents that have the software you need to build your app.

1. For the **Yaml path**, select the **.vsts-ci.yml** file in the root of your repo.

1. Select the **Triggers** tab, and then enable continuous integration (CI).

1. Save and queue the build, and then choose the number of the build: _{year}{month}{day}.1_ that has been queued.

1. In the left column of the running build, select **Job**. After an agent is assigned to your job and the agent is initialized, then you'll see information about the build in the console.

[//]: # (TODO: Add link to GitHub tutorial after advice is added there on authentication)

---

## View the build summary

[!INCLUDE [include](../apps/_shared/view-build-summary.md)]

## Next steps

You've just learned the basics to create and run a CI build pipeline in YAML.
This pipeline automatically builds and validates whatever code is checked in by your team. 
Now you're ready to learn how to configure your pipeline for the programming language you're using.

[//]: # (TODO: Add links to language topics)