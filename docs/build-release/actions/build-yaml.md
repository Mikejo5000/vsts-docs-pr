---
title: CI Build in code using YAML
description: Define your CI build process in YAML in Visual Studio Team Services (VSTS) and Team Foundation Server (TFS)
ms.prod: vs-devops-alm
ms.technology: vs-devops-build
ms.assetid: 5A3A363E-C21F-4593-A145-B57492E9FEDC
ms.manager: douge
ms.author: alewis
ms.date: 11/11/2017
---

# Configure your CI Build in code using YAML

**VSTS**

When you define a CI build on VSTS, you've got a fundamental choice: use a web-based interface or configure your CI process as code in a YAML build. YAML build definitions give you the advantages of _configuration as code_. 

In a YAML build definition, your CI build process is versioned with your code. This means: 

* If a change to the build process causes a break or results in an unexpected outcome, you can much more easily identify the issue because the change is in version control with the rest of your codebase. This way you can more clearly see the issue and fix it like any other kind of bug.

* It's easier to copy and paste from one build definition into another.

* People who prefer to work in code are more comfortable with this kind of build definition.

> [!TIP]
> If you're new to YAML builds, or to VSTS, we suggest you [begin with our tutorial](build-yaml-get-started.md) and then come back here.

## How do YAML builds compare to web-interface builds?

[//]: # (TODO: review https://github.com/Microsoft/vsts-agent/blob/master/docs/preview/yamlgettingstarted-features.md with PM; brainstorm for other gaps)

|Capability|YAML|Web interface|
|-|-|-|
|<center>**Repository**</center>|
|Git and GitHub|Yes|Yes|
|TFVC|No|Yes|
|Bitbucket, external Git, Subversion|No|Yes|
|<center>**Capabilities**</center>|
|Fan out and fan in|Yes|No|
|Test and debug the process locally|Yes|No|
|Inline bash scripts|Yes|No|

## Create a YAML build definition

To make it more convenient to create YAML build definitions, VSTS automatically creates a definition when you add a file named .vsts-ci.yml to the root of your resository. It creates the build definition in a folder that has the same name as your repository.

1. Navigate to the **Code** hub, choose the **Files** tab, and then choose the repository you created in the above steps.

1. In the root folder of the repo, create a new file called **.vsts-ci.yml**.

1. Paste the following content into the file:

```YAML
steps:
- script: echo hello world 
```

1. A new build is automatically created.

 > [!NOTE]
 > If your team project already has a build definition that's pointing to the file, then the system does not automatically create another build definition.


To see a more interesting example in action:

1. Replace the file with this content:

```YAML
steps:

- script: |
    echo hello world from %MyName%
    echo Agent.HomeDirectory is %CD%
  workingDirectory: $(Agent.HomeDirectory)
  env:
    MyName: $(Agent.MachineName)
  condition: and(succeeded(), eq(variables['agent.os'], 'windows_nt'))
  displayName: Greeting from Windows machine

- script: |
    echo hello world from $MyName
    echo Agent.HomeDirectory is $PWD
  workingDirectory: $(Agent.HomeDirectory)
  env:
    MyName: $(Agent.MachineName)
  condition: and(succeeded(), in(variables['agent.os'], 'darwin', 'linux'))
  displayName: Greeting from macOS or Linux machine
```

1. Queue the build on any of our hosted agent pools, including **Hosted VS 2017**, **Hosted Linux Preview** or **Hosted macOS Preview**.

## Create an artifact

This build archives your entire repo into a .ZIP file and publishes it as an artifact.

```YAML
steps:

- archiveFiles@1
  rootFolder: $(Build.SourcesDirectory)
  displayName: Zip it
 # default value for archiveFile is $(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip
 
- publishBuildArtifacts@1
  pathToPublish: $(Build.ArtifactStagingDirectory)
  artifactName: drop
  artifactType: Container
```

Notice how you don't have to supply the default arguments.

## Look up tasks

To look up the syntax of the tasks that are built into VSTS and TFS, see https://github.com/Microsoft/vsts-tasks/tree/master/Tasks. 

For example, if you want to use the [Copy Files](../tasks/utility/copy-files.md) task, go to https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/CopyFiles and then click the **task.json** file. In this file you'll find the name of task, which in this case is `CopyFiles`. You'll also find the valid `inputs`, for example the `SourceFolder` input.

