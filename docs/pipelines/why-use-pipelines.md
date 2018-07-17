---
title: Why Use Azure DevOps Pipelines?
description: Determine how Azure DevOps Pipelines can improve your coding environment and code delivery.
ms.prod: devops
ms.technology: devops-cicd
ms.manager: douge
ms.author: douge
ms.date: 07/06/2018
monikerRange: '>= tfs-2015'
---

# Why Use Azure DevOps Pipelines?

Azure DevOps Pipelines is the quickest, easiest, and safest way to automate building your projects and making them available to users.

There are two main components of Pipelines: Continuous Integration (CI) and Continous Delivery (CD).

**Continous Integration (CI)**: CI is the practice used by development teams to automate the merging and testing of code. Implementing CI helps to catch bugs early in the development cycle, which makes them less expensive to fix. Automated tests execute as part of the CI process to ensure quality. Artifacts are produced from CI systems and fed to release pipelines to drive frequent deployments. The Build service in VSTS and TFS helps you set up and manage CI for your applications.

**Continuous Delivery (CD)**: CD is a process by which code is built, tested, and deployed to one or more test and production environments. Deploying and testing in multiple environments drives quality. CI systems produce the deployable artifacts including infrastructure and apps. Automated release pipelines consume these artifacts to release new versions and fixes to existing systems. Monitoring and alerting systems run continually to drive visibility into the entire CD process. The Release service in VSTS and TFS helps you set up and manage CD for your applications.

## What can Pipelines do?

Maybe a list or a table that has things like:

* Automate building of your project to ensure it stays up to date and error-free
* Automate packaging of your project to make the newest version available to all users
* etc.

AKA, what problems do I have that I can solve with Pipelines

### App developer that wants to push weekly updates

### .NET developer that ships their code via packages

### etc.

