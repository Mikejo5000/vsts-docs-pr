---
title: Azure DevOps Pipelines New User Guide  
description: Learn the basics about Azure DevOps Pipelines and how to use it to automatically build and release code.
ms.prod: devops
ms.technology: devops-cicd
ms.manager: douge
ms.author: douge
ms.date: 07/06/2018
monikerRange: '>= tfs-2015'
---

# Azure DevOps Pipelines New User Orientation

Azure DevOps Pipelines is a cloud service that you can use to automatically build your code project and make it available to other users. It works with just about any language or project type.

If you're not sure if Pipelines is right for your needs, read [Why Use Azure DevOps Pipelines?](why-use-pipelines.md).

## What is Pipelines

There are two main components of Pipelines: Continuous Integration (CI) and Continous Delivery (CD).

**Continous Integration (CI)**: CI is the practice used by development teams to automate the merging and testing of code. Implementing CI helps to catch bugs early in the development cycle, which makes them less expensive to fix. Automated tests execute as part of the CI process to ensure quality. Artifacts are produced from CI systems and fed to release pipelines to drive frequent deployments.

**Continuous Delivery (CD)**: CD is a process by which code is built, tested, and deployed to one or more test and production environments. Deploying and testing in multiple environments drives quality. CI systems produce the deployable artifacts including infrastructure and apps. Automated release pipelines consume these artifacts to release new versions and fixes to existing systems. Monitoring and alerting systems run continually to drive visibility into the entire CD process.

## Does Pipelines work with my language and tools?

### Languages

You can use practically any language with Azure DevOps Pipelines, including **Java, C#, C++, Python, Go, and Ruby.**

### Version control systems

The starting point for configuring CI and CD for your applications is to have your source code in a version control system. Pipelines supports two forms of version control: **Git and Team Foundation Version Control.**

### Application types

You can use Azure DevOps Pipelines with most application types, including **.NET, Java, Node, Android, Xcode, and C++.**

### Deployment targets: 

Azure DevOps Pipelines can be used to deploy your code to multiple targets, such as **virtual machines, containers, on-premises and cloud platforms, PaaS services.**

### Package formats: NuGet, npm, Maven

If your goal is to produce packages that can be consumed by others, you can publish **NuGet, npm, or Maven packages** to the build-in package management repository in VSTS or any other package management repository of your choice.

## What do I need to use Pipelines?

Insert table here of any required tools/software to use Pipelines. Could change based off of scenario.

## How do I start using Pipelines?

This is important. We need to drive home that Pipelines can change based on scenario but that ALL scenarios can be executed easily. This should probably link to a "get started" guide, or maybe multiple if we can, based on scenarios.

## Resources