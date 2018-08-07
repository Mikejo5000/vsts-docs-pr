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
layout: LandingPage
monikerRange: 'vsts'
---

# What is Azure Repos?

Host and manage your code in Azure Repos. Whether your software project is large or small, using version control as soon as possible is a good idea. Version control systems are software that help you track changes you make in your code over time. As you edit your code, you tell the version control system to take a snapshot of your files. The version control system saves that snapshot permanently so you can recall it later if you need it. Use version control to save your work and coordinate code changes across your team. Even if you're just a single developer, version control helps you stay organized as you fix bugs and develop new features. Version control keeps a history of your development so that you can review and even rollback to any version of your code with ease.

Azure Repos provides two types of version control:

- [Git](#git) - distributed version control
- [TFVC](#TFVC) - centralized version control

## Git

Git is the most commonly used version control system today and is quickly becoming the standard for version control. Git is a distributed version control system, meaning your local copy of code is a complete version control repository. These fully functional local repositories make it is easy to work offline or remotely. You commit your work locally, and then sync your copy of the repository with the copy on the server.

Git in Azure Repos is standard Git. You can use the clients and tools of your choice, such as Git for Windows, Mac, third part Git services, and tools such as Visual Studio and Visual Studio Code.


<div class="row">
<div class="col-sm-6 col-md-6">
![Use your favorite IDE with VSTS and Git](_img/overview/get-started-favorite-ide.png)
</div>
<div class="col-sm-6 col-md-6">

<p>Connect your favorite development environment to VSTS to access your repos and manage your work.
VSTS IDE integrations are available for [Visual Studio](../../organizations/accounts/set-up-vs.md), 
[Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vsts.team), [Eclipse](/vsts/java/download-eclipse-plug-in), 
and [IntelliJ](/vsts/java/download-intellij-plug-in).</p>


<p>New to Git? Learn how to share code with Azure Repos with the following getting started guides:</p>
</div>
</div>

<!--- All images are Placeholder --> 
<!-- Converting to icon48 format, this gets cleaner in YAML -->
<div class="ico48Case halfStack"><div class="ico48Link"><a href="create-new-repo.md"><img width="48" height="48" alt="" src="https://docs.microsoft.com/media/common/i_web.svg"><span>Web</span></a></div><div class="ico48Link"><a href="share-your-code-in-git-vs-2017.md"><img width="48" height="48" alt="" src="https://docs.microsoft.com/media/logos/logo_visual-studio.svg"><span>Visual Studio</span></a></div><div class="ico48Link"><a href="share-your-code-in-git-cmdline.md"><img width="48" height="48" alt="" src="https://docs.microsoft.com/media/common/i_cligeneric.svg"><span>Command-line</span></a></div><div class="ico48Link"><a href="share-your-code-in-git-xcode.md"><img width="48" height="48" alt="" src="https://docs.microsoft.com/media/logos/logo_xcode.svg"><span>Xcode</span></a></div><div class="ico48Link"><a href="share-your-code-in-git-eclipse.md"><img width="48" height="48" alt="" src="https://docs.microsoft.com/media/logos/logo_eclipse.svg"><span>Eclipse</span></a></div>

<div class="ico48Link"><a href="create-repo-intellij.md"><img width="48" height="48" alt="" src="https://docs.microsoft.com/en-us/media/logos/logo_intellij.svg"><span>IntelliJ</span></a></div>

</div>

### Git tutorial

<div class="row">
<div class="col-sm-6 col-md-6">
<p>Get up and running with Git and VSTS in just a few minutes with the [VSTS Git quick start](gitquickstart.md).</p>

<p>The [VSTS Git tutorial](gitworkflow.md) walks you through Git tasks like [creating repos](creatingrepo.md), [working in branches](branches.md), [saving your work](commits.md), and [sharing your changes](pushing.md). 
Every task is presented step-by-step in Visual Studio or from the command line.</p>
</div>
<div class="col-sm-6 col-md-6">
![VSTS Git tutorial workflow](_img/gitworkflow.png)

</div>
</div>   

### Authenticate with your repos

<div class="row">
<div class="col-sm-6 col-md-6">

![Connect to VSTS from anywhere](_img/overview/IC839946.png)   

</div>

<div class="col-sm-6 col-md-6"> 

<p>You can authenticate with your VSTS Git repo from any platform using [cross-platform credential managers](set-up-credential-managers.md) or [SSH public key authentication](use-ssh-keys-to-authenticate.md).</p>

<p>If you have code ready to share in VSTS, our getting started guides take you through the steps to connect your development environment to a VSTS Git repo and share your code with your team.</p>

<ul>
<li>[Get Started with Visual Studio](share-your-code-in-git-vs.md)</li>
<li>[Get Started with Xcode](share-your-code-in-git-xcode.md)</li>
<li>[Get Started with Eclipse](share-your-code-in-git-eclipse.md)</li>
<li>[Get Started with IntelliJ](create-repo-intellij.md)</li>
</ul>

</div>
</div>

### Manage your repos

<div class="row">
<div class="col-sm-6 col-md-6"> 
<p>Manage your repos and customize your team's workflow. Set up permissions to control access to your code and set up branch policies and continuous integration to prevent build breaks and catch bugs sooner.</p>

<ul>
<li>[Create](create-new-repo.md), [delete](delete-existing-repo.md), and [rename](repo-rename.md) repos.</li>
<li>Set [repo permissions](../../organizations/security/permissions.md) and [branch permissions](branch-permissions.md)</li>
<li>[Set up branch policies](branch-policies.md) to protect key branches</li>
<li>[Set up continuous integration](../../pipelines/build/triggers.md#continuous-integration-ci) to catch bugs sooner.</li>
</ul>

</div>
<div class="col-sm-6 col-md-6"> 

![Manage your code and repos from the web](_img/overview/git-repos.png)

</div>
</div>

### Review code

<div class="row">
<div class="col-sm-6 col-md-6">

![Review code with pull requests in VSTS and TFS](_img/overview/pull-request.png)

</div>
<div class="col-sm-6 col-md-6"> 

<p>Review code with your team and make sure that changes build and pass tests before it's merged.</p>

<ul class="panelContent cardsFTitle">
    <li>
        <a href="pull-requests.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="https://docs.microsoft.com/media/common/i_pull-request.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Create a pull request</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="pull-requests.md#link-work-items">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="../../_img/index/i_tasks.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Link work items to pull requests</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="branch-policies.md#build-validation">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="../../_img/index/i_branch-policies.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Set up branch policies</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="merging-with-squash.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="https://docs.microsoft.com/media/common/i_pull-request.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Squash merge pull requests</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="git-branching-guidance.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="../../_img/index/i_branch-policies.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Git branch and pull request workflows</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
</ul>

</div>
</div>

## Pull requests

Pull requests combine the review and merge of your code into a single collaborative process.
Once you're done fixing a bug or new feature in a branch, create a new pull request.
Add the members of the team to the pull request so they can review and vote on your changes.

VSTS has a [rich pull request experience](pull-requests.md) that's easy to use and scales to your needs.
Use pull requests to review works in progress and get early feedback on changes.
There's no commitment to merge the changes as the owner can abandon the pull request at any time.

### Get your code reviewed

The code review done in a pull request isn't just to find obvious bugs.
That's what your tests are for.
A good code review catches less obvious problems that could lead to costly issues later.
Code reviews help protect your team from bad merges and broken builds that sap your team's productivity.
The review catches these problems before the merge, protecting your important branches from unwanted changes.

Cross-pollinate expertise and spread problem solving strategies by using a wide range of reviewers in your code reviews.
Diffusing skills and knowledge makes your team stronger and more resilient.

<ul class="panelContent cardsFTitle">
    <li>
        <a href="pullrequest.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="https://docs.microsoft.com/media/common/i_pull-request.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Review code with pull requests</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="pull-requests.md#link-work-items">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="../../_img/index/i_tasks.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Link work items to pull requests</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
</ul>

### Give great feedback

High quality reviews start with high quality feedback.
The keys to great feedback in a pull request are:

* Have the right people review the pull request
* Make sure that reviewers know what the code does
* Give actionable, constructive feedback
* Reply to comments in a timely manner

When assigning reviewers to your pull request, make sure you select the right set of reviewers.
You want reviewers that will know how your code works, but try to also include developers working in other areas so they can share their ideas.
Provide a clear description of your changes and provide a build of your code that has your fix or feature running in it.

Reviewers should make an effort to provide feedback on changes they don't agree with.
Identify the issue and give a specific suggestions on what you would do differently.
This feedback has clear intent and is easy for the owner of the pull request to understand.
The pull request owner should reply to the comments, accepting the suggestion or explaining why the suggested change isn't ideal.
Sometimes a suggestion is good, but the changes are outside the scope of the pull request.
Take these suggestions and create new work items and feature branches separate from the pull request to make those changes.

<ul class="panelContent cardsFTitle">
        <li>
        <a href="pull-requests.md#leave-comments">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="https://docs.microsoft.com/media/common/i_blog.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Leave comments</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="pull-requests.md#vote-on-the-changes">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="_img/logos/check.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Vote on the changes</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
</ul>

### Protect branches with policies

There are a few critical branches in your repo that the team relies on always being in good shape, such as your `master` branch.
[Require pull requests](branch-policies.md) to make any changes on these branches.
Developers pushing changes directly to the protected branches will have their pushes rejected.

Add additional conditions to your pull requests to enforce a higher level of code quality in your key branches.
A clean build of the merged code and approval from multiple reviewers are some extra requirements you can set to protect your key branches.

<ul class="panelContent cardsFTitle">
    <li>
        <a href="branch-policies-overview.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="../../_img/index/i_branch-policies.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Branch policies overview</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="branch-policies.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="https://docs.microsoft.com/media/common/i_policy.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>How to configure branch policies</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="branch-permissions.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="https://docs.microsoft.com/media/common/i_protect.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Branch permissions</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
</ul>

### Extend pull request workflows with pull request status

Pull requests and branch policies enable teams to enforce many best practices related to reviewing code and running automated builds, but many teams have additional requirements and validations to perform on code. To cover these individual and custom needs, VSTS offers pull request statuses. Pull request statuses integrate into the PR workflow and allow external services to programmatically sign off on a code change by associating simple success/failure type information with a pull request. 

<ul class="panelContent cardsFTitle">
    <li>
        <a href="pull-request-status.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="https://docs.microsoft.com/media/common/i_pull-request.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Pull request status overview</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="create-pr-status-server.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="https://docs.microsoft.com/media/common/nodejs.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Create a PR status server with Node.js</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="create-pr-status-server-with-azure-functions.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="https://docs.microsoft.com/en-us/azure/media/index/azurefunctions.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Use Azure Functions to create custom branch policies</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="pr-status-policy.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="https://docs.microsoft.com/media/common/i_web.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Configure a branch policy for an external service</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
</ul>

### Videos 
> [!VIDEO https://www.youtube.com/embed/J_DHkUKxI0E?start=0]

## Branch policies

Branch policies are an important part of the Git workflow and enable you to:

* Isolate work in progress from the completed work in your master branch
* Guarantee changes build before they get to master
* Limit who can contribute to specific branches
* Enforce who can create branches and the naming guidelines for the branches
* Automatically include the right reviewers for every code change
* Enforce best practices with required code reviewers

### Adopt a Git branching strategy

There are a few critical branches in your repo that the team relies on always being in good shape, such as your `master` branch.
[Require pull requests](branch-policies.md) to make any changes on these branches.
Developers pushing changes directly to the protected branches will have their pushes rejected.

Keep your branch strategy simple by building your strategy from these three concepts:

0. Use feature branches for all new features and bug fixes.
0. Merge feature branches into the master branch using pull requests. 
0. Keep a high quality, up-to-date master branch.  

A strategy that extends these concepts and avoids contradictions will result in a version control workflow for your team that is consistent and easy to follow. 

<ul class="panelContent cardsFTitle">
    <li>
        <a href="git-branching-guidance.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="../../_img/index/i_branch-policies.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Adopt a branching strategy</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="branch-policies.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="https://docs.microsoft.com/media/common/i_policy.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>How to configure branch policies</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="branch-permissions.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="https://docs.microsoft.com/media/common/i_protect.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Branch permissions</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="require-branch-folders.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="_img/logos/folder.png" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Require branch folders</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="pr-status-policy.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="https://docs.microsoft.com/media/common/i_web.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Configure a branch policy for an external service</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
</ul>

### Branching how to guides

Learn how to perform common tasks when working with branches.

<ul class="panelContent cardsFTitle">
    <li>
        <a href="branches.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="../../_img/index/i_branch-policies.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Branches tutorial</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="create-branch.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="_img/logos/add.png" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>How to create a branch</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="delete-branch.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="_img/logos/delete.png" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>How to delete a branch</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="restore-deleted-branch.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="_img/logos/restore.png" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Restore a deleted branch</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="lock-branches.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="_img/logos/lock-branches.png" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>How to lock branches</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
</ul>




## Forks

Forks are a great way to isolate experimental, risky, or confidential changes from the original codebase. A fork is a complete copy of a repository, including all files, commits, and (optionally) branches. The new fork acts as if someone cloned the original repository, then pushed to a new, empty repository.
After a fork has been created, new files, folders, and branches are not shared between the repositories unless a pull request carries them along. Once you're ready to share those changes, it's easy to use [pull requests](pull-requests.md) to push the changes back to the original repository.

### The forking workflow

When working with forks, you typically use the following workflow:

1. [Create a fork](forks.md#create-fork)
2. [Clone it locally](forks.md#clone-locally)
3. [Make your changes locally and push them to a branch](forks.md#push-changes)
4. [Create and complete a PR to upstream](forks.md#create-pr)
5. [Sync your fork to the latest from upstream](forks.md#sync-fork)


### Learn more

<ul class="panelContent cardsFTitle">
    <li>
        <a href="forks.md">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img width="48" height="48" alt="" src="https://docs.microsoft.com/media/common/i_forks.svg" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Learn more about forks</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
 </ul>

## Public projects


