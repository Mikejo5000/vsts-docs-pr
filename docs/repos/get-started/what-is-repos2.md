---
title: Collaborate on code
titleSuffix: Azure DevOps Services
description: What do you get with Azure Repos  
ms.prod: devops
ms.technology: devops-new-user
ms.manager: douge
ms.author: sdanie
author: steved0x
ms.date: 09/05/2018
ms.topic: overview
monikerRange: 'vsts'
---

# What is Azure Repos?

Azure Repos is a set of version control tools you can use to manage your code. Whether your software project is large or small, using version control as soon as possible is a good idea. Version control systems are software that help you track changes you make in your code over time. As you edit your code, you tell the version control system to take a snapshot of your files. The version control system saves that snapshot permanently so you can recall it later if you need it. Use version control to save your work and coordinate code changes across your team. Even if you're just a single developer, version control helps you stay organized as you fix bugs and develop new features. Version control keeps a history of your development so that you can review and even rollback to any version of your code with ease.

Azure Repos provides two types of version control:

- [Git](#git) - distributed version control
- [TFVC](#TFVC) - centralized version control

## Git

Git is the most commonly used version control system today and is quickly becoming the standard for version control. Git is a distributed version control system, meaning your local copy of code is a complete version control repository. These fully functional local repositories make it is easy to work offline or remotely. You commit your work locally, and then sync your copy of the repository with the copy on the server.

Git in Azure Repos is standard Git. You can use the clients and tools of your choice, such as Git for Windows, Mac, third part Git services, and tools such as Visual Studio and Visual Studio Code.

## Connect your favorite development environment

Connect your favorite development environment to Azure Repos to access your Git repos and manage your work.

- [Git command line](../git/share-your-code-in-git-cmdline.md)
- [Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vsts.team)
- [Visual Studio](../git/share-your-code-in-git-vs-2017.md)
- [Xcode](../git/share-your-code-in-git-xcode.md)
- [Eclipse](/vsts/java/download-eclipse-plug-in)
- [IntelliJ](/vsts/java/download-intellij-plug-in)

## Review code with pull requests

Review code with your team and make sure that changes build and pass tests before it's merged. Pull requests combine the review and merge of your code into a single collaborative process.
Once you're done fixing a bug or new feature in a branch, create a new pull request.
Add the members of the team to the pull request so they can review and vote on your changes.

VSTS has a [rich pull request experience](../git/pull-requests-overview.md) that's easy to use and scales to your needs.
Use pull requests to review works in progress and get early feedback on changes.
There's no commitment to merge the changes as the owner can abandon the pull request at any time.

- [Create a pull request](../git/pull-requests-overview.md)
- [Link work items to pull requests](../git/pull-requests.md#link-work-items)
- [Require build validation with branch policies](../git/branch-policies.md#build-validation)
- [Squash merge pull requests](../git/merging-with-squash.md)
- [Git branching guidance](../git/git-branching-guidance.md)
- [Leave comments](../git/pull-requests.md#leave-comments)
- [Vote on the changes](../git/pull-requests.md#vote-on-the-changes)

## Protect branches with policies

There are a few critical branches in your repo that the team relies on always being in good shape, such as your `master` branch.
[Require pull requests](../git/branch-policies.md) to make any changes on these branches.
Developers pushing changes directly to the protected branches will have their pushes rejected.

Add additional conditions to your pull requests to enforce a higher level of code quality in your key branches.
A clean build of the merged code and approval from multiple reviewers are some extra requirements you can set to protect your key branches.

- [Branch policies overview](../git/branch-policies-overview.md)
- [How to configure branch policies](../git/branch-policies.md)
- [Branch permissions](../git/branch-permissions.md)

## Extend pull request workflows with pull request status

Pull requests and branch policies enable teams to enforce many best practices related to reviewing code and running automated builds, but many teams have additional requirements and validations to perform on code. To cover these individual and custom needs, VSTS offers pull request statuses. Pull request statuses integrate into the PR workflow and allow external services to programmatically sign off on a code change by associating simple success/failure type information with a pull request. 

- [Pull request status overview](../git/pull-request-status.md)
- [Create a PR status server with Node.js](../git/create-pr-status-server.md)
- [Use Azure Functions to create custom branch policies](../git/create-pr-status-server-with-azure-functions.md)
- [Configure a branch policy for an external service](../git/pr-status-policy.md)

## Isolate code with forks

Forks are a great way to isolate experimental, risky, or confidential changes from the original codebase. A fork is a complete copy of a repository, including all files, commits, and (optionally) branches. The new fork acts as if someone cloned the original repository, then pushed to a new, empty repository.
After a fork has been created, new files, folders, and branches are not shared between the repositories unless a pull request carries them along. Once you're ready to share those changes, it's easy to use [pull requests](../git/pull-requests-overview.md) to push the changes back to the original repository.

- [Learn more about forks](../git/forks.md)

## TFVC

Azure Repos also supports Team Foundation Version Control (TFVC). TFVC is a centralized version control system. Typically, team members have only one version of each file on their dev machines. Historical data is maintained only on the server. Branches are path-based and created on the server.

- [Learn more about TFVC](../tfvc/index.md)

Get started by creating a project, configuring your workspace, and reviewing and sharing your code. You can use any one of these clients or IDEs: 

- [Visual Studio](../tfvc/share-your-code-in-tfvc-vs.md)
- [Xcode](../tfvc/share-your-code-in-tfvc-xcode.md)
- [Eclipse](../tfvc/share-your-code-in-tfvc-eclipse.md)