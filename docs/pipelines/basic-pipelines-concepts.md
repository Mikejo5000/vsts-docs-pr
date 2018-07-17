---
title: Azure DevOps Pipelines New User Guide - Key Concepts
description: Learn how Azure DevOps Pipelines works with your code and tools to automate build and deploy, and the key concepts behind it.
ms.prod: devops
ms.technology: devops-cicd
ms.manager: douge
ms.author: douge
ms.date: 07/06/2018
monikerRange: '>= tfs-2015'
---

# Key Concepts for New Azure DevOps Pipelines Users

Learn about the key concepts and components that are used in Pipelines. Understanding the basic terms and parts of Pipelines will help you further explore how it can help you deliver better code more efficiently and reliably.

## Key terms

### What is 'build'?

### What is 'release'?

### What is 'continuous integration'?

**Continuous Integration (CI)** is the practice used by development teams to automate the merging and testing of code. Implementing CI helps to catch bugs early in the development cycle, which makes them less expensive to fix. Automated tests execute as part of the CI process to ensure quality. Artifacts are produced from CI systems and fed to release pipelines to drive frequent deployments. The Build service in VSTS and TFS helps you set up and manage CI for your applications.

### What is 'continuous delivery'?

**Continuous Delivery (CD)** is a process by which code is built, tested, and deployed to one or more test and production environments. Deploying and testing in multiple environments drives quality. CI systems produce the deployable artifacts including infrastructure and apps. Automated release pipelines consume these artifacts to release new versions and fixes to existing systems. Monitoring and alerting systems run continually to drive visibility into the entire CD process. The Release service in VSTS and TFS helps you set up and manage CD for your applications.

### What is a 'pipeline'?

A **pipeline** is a representation of the automation process that you want to run to build and test (build pipeline) or deploy (release pipeline) your application. A pipeline is defined as a collection of tasks.

### What is a 'task'?

A **task** is the building block of a pipeline. For example, a build pipeline may consists of build tasks and test tasks, while a release pipeline will consist of deployment tasks.

### What is an 'agent'?

## How Pipelines works

![Pipelines into image](./_img/pipelines-image.png)

Azure DevOps Pipelines is simple in its design:

1. Edit your code any way you like
2. Push your code to your version control repository
3. Once your code is pushed to the repository, your build pipeline is triggered
    * Any tasks in your build pipeline (checking and testing code) will be run
4. The build pipeline creates an artifact that is used by the release pipeline
    * Any tasks (deploying code) in your release pipeline will be run
5. Your updated, tested, and packaged code is sent to your deployment target






