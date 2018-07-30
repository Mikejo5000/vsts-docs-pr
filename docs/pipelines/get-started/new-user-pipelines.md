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

Azure DevOps Pipelines is a cloud service that you can use to automatically build and test your code project and make it available to other users. It works with just about any language or project type.

If you're not sure if Pipelines is right for your needs, read [Why Use Azure DevOps Pipelines?](why-use-pipelines.md).

## What is Azure DevOps Pipelines?

There are two main parts of Pipelines: Continuous Integration (CI) and Continous Delivery (CD).

**Continous Integration (CI)**: CI is the practice used by development teams to simplify the merging and testing of code. CI helps to catch bugs or problems early in the development cycle, which makes them easier and faster to fix. Automated tests are run as part of the CI process to ensure quality. Items known as "artifacts" are produced from CI systems and used by the **Continuous Delivery** release pipelines to drive automatic deployments.

**Continuous Delivery (CD)**: CD is a process by which code is built, tested, and deployed to one or more test and production environments. Deploying and testing in multiple environments drives quality. CI systems produce the deployable artifacts, including infrastructure and apps, automated release pipelines consume these artifacts to release new versions and fixes to existing systems. Monitoring and alerting systems run constantly to drive visibility into the entire CD process and to ensure errors are caught often and early.

## Does Pipelines work with my language and tools?

### Languages

You can use practically any language with Azure DevOps Pipelines, including **Java, C#, C++, Python, Go, and Ruby.**

### Version control systems

The starting point for using CI and CD practices for your applications is to have your source code in a version control system. Pipelines supports two forms of version control: **Git and Team Foundation Version Control.**

### Application types

You can use Azure DevOps Pipelines with most application types, including **.NET, Java, Node, Android, Xcode, and C++.**

### Deployment targets

Azure DevOps Pipelines can be used to deploy your code to multiple targets, such as **virtual machines, containers, on-premises and cloud platforms, PaaS services.**

### Package formats

If your goal is to produce packages that can be consumed by others, you can publish **NuGet, npm, or Maven packages** to the built-in package management repository in VSTS or any other package management repository of your choice.

## What do I need to use Pipelines?

To use Azure DevOps Pipelines, you'll need the following:

* A VSTS or TFS account
* Have your source code stored in a version control system (Git or TFVC)

## How do I start using Pipelines?

If you'd like to ramp up and learn a little more about Pipelines, visit our get started guide to [Create your first build and release flow](../get-started-designer.md).

If you'd like to jump in and use Pipelines with your code, check out....

## Resources