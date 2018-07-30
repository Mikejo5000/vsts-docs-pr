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

## How Pipelines works

![Pipelines into image](../_img/pipelines-image.png)

Azure DevOps Pipelines is simple in its design:

1. Edit your code any way you like
2. Push your code to your version control repository
3. Once your code is pushed to the repository, your build pipeline is triggered
    * Any tasks in your build pipeline (checking and testing code) will be run
4. The build pipeline creates an artifact that is used by the release pipeline
    * Any tasks (deploying code) in your release pipeline will be run
5. Your updated, tested, and packaged code is sent to your deployment target

## Key terms

### What is 'build'?

### What is 'release'?

### What is 'continuous integration'?

**Continuous Integration (CI)** CI is the practice used by development teams to simplify the merging and testing of code. CI helps to catch bugs or problems early in the development cycle, which makes them easier and faster to fix. Automated tests are run as part of the CI process to ensure quality. Items known as "artifacts" are produced from CI systems and used by the **Continuous Delivery** release pipelines to drive automatic deployments.

### What is 'continuous delivery'?

**Continuous Delivery (CD)**: CD is a process by which code is built, tested, and deployed to one or more test and production environments. Deploying and testing in multiple environments drives quality. CI systems produce the deployable artifacts, including infrastructure and apps, automated release pipelines consume these artifacts to release new versions and fixes to existing systems. Monitoring and alerting systems run constantly to drive visibility into the entire CD process and to ensure errors are caught often and early.

### What is a 'pipeline'?

A **pipeline** is a representation of the automation process that you want to run to build and test (build pipeline) or deploy (release pipeline) your application. A pipeline is defined as a collection of tasks.

### What is a 'task'?

A **task** is the building block of a pipeline. For example, a build pipeline may consists of build tasks and test tasks, while a release pipeline will consist of deployment tasks.

### What is an 'agent'?

When your build or deployment runs, the system begins one or more jobs. An **agent** is installable software that runs one build or deployment job at a time.

The [Build and Release Agents article](../agents/agents.md) goes more in-depth about the different types of agents and how to use them.

### What is a 'deployment target'?

Once you have continuous integration in place, the next step is to create a release pipeline to automate the deployment of your application to one or more environments. This automation process is again defined as a collection of tasks. VSTS and TFS support deploying your application to virtual machines, containers, on-premises and cloud platforms, or PaaS services. You can also publish your mobile application to a store.








