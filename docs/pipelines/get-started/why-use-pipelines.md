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

## The importance of Continuous Integration (CI) and Continuous Delivery (CD) pipelines in software development

There are two main parts of Pipelines: Continuous Integration (CI) and Continous Delivery (CD).

**Continous Integration (CI)**: CI is the practice used by development teams to simplify the merging and testing of code. CI helps to catch bugs or problems early in the development cycle, which makes them easier and faster to fix. Automated tests are run as part of the CI process to ensure quality. Items known as "artifacts" are produced from CI systems and used by the **Continuous Delivery** release pipelines to drive automatic deployments.

**Continuous Delivery (CD)**: CD is a process by which code is built, tested, and deployed to one or more test and production environments. Deploying and testing in multiple environments drives quality. CI systems produce the deployable artifacts, including infrastructure and apps, automated release pipelines consume these artifacts to release new versions and fixes to existing systems. Monitoring and alerting systems run constantly to drive visibility into the entire CD process and to ensure errors are caught often and early.

### Quick look at CI/CD benefits

| Continuous Integration (CI)                    |  Continous Delivery (CD)                       |
| -----------------------------------------------|------------------------------------------------|
| Increase code coverage                         | Automatically deploy code to production        |
| Build stuff faster by splitting test and build | Ensure deployment targets have latest code     |
| Automatically ensure you don't ship broken code| Use tested code from CI process
| Run tests continually                          |

## Why use Azure DevOps Pipelines for CI and CD

* Works with any language or platform
* Deploy to different types of targets at the same time
* Best integration experience for deploying to Azure
* Build on Windows, Linux, or Mac machines
* Great integration for GitHub
* Great offer for OSS repos

## What can Pipelines do for me?

### Development process _without_ Azure Devops Pipelines


> **ELBATK NOTE**: AKA, what problems do I have that I can solve with Pipelines

### Automate building and testing of your project to ensure it stays up to date and error-free

### Automate the deployment of your built and tested project to numerous targets such as an app store, or a package management respository

### Automate packaging of your project to make the newest version available to all users

