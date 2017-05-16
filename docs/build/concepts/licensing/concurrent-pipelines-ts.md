---
title: Build and Release Management concurrent pipelines in Visual Studio Team Services
description: Build and Release Management concurrent pipelines in Visual Studio Team Services (VSTS)
ms.assetid: FAFB2DE4-F462-4E9E-8312-4F343F2A35B8
ms.prod: vs-devops-alm
ms.technology: vs-devops-build
ms.manager: douge
ms.author: alewis
ms.date: 10/20/2016
---
# Concurrent build and release pipelines in Visual Studio Team Services

**[TFS 2017](concurrent-pipelines-tfs.md) | Team Services**

A Team Services _concurrent pipeline_ gives you the ability to run a single build or a single release at a time in your account.

We provide one free concurrent pipeline in each Team Services account. We also provide 240 minutes of total compute time per month from a [hosted agent](../../concepts/agents/hosted.md) to run a build or a release. Each build or release job cannot run for more than 30 minutes.

For no additional charge you can keep hundreds or even thousands of build and release definitions in your account. You also can register any number of [private agents](../../concepts/agents/agents.md#install) with your account for no additional charge.

To run more than one build or release at a time, you need additional concurrent pipelines, which you can buy from the Visual Studio Marketplace.

## How a concurrent pipeline is consumed

For example, a Team Services account has one concurrent pipeline. This allows users in that account to run only one build or release at a time. When additional builds and releases are triggered, they are queued and will wait for the previous one to complete.

A release requires a concurrent pipeline only when it is being actively deployed to an environment. Waiting for an approval or a manual intervention does not consume a concurrent pipeline.

![Concurrent pipelines simple example](_img/concurrent-pipelines-vsts/concurrent-pipelines-simple-example.png)

0. FabrikamFiber CI Build 102 (master branch) is first to be started.
0. Deployment of FabrikamFiber Release 11 is triggered by completion of FabrikamFiber CI Build 102.
0. FabrikamFiber CI Build 101 (feature branch) is triggered. The build can't start yet because Release 11's deployment is active. So the build stays queued.
0. Release 11 waits for approvals. Fabrikam CI Build 101 starts because a release waiting for approvals does not consume a concurrent pipeline.
0. Release 11 is approved. It resumes only after Fabrikam CI Build 101 is completed.

## Concurrent processing within a single build or release

Concurrent processing within a single build or release does not require additional concurrent pipelines. So long as you have enough agents, you can

* In a build process, run multiple build configurations at the same time.

* In a release process, deploy to multiple environments at the same time.

For example, suppose your Team Services account has three concurrent pipelines. You can have more than three agents running at the same time to perform parallel operations within builds and releases. For instance, notice below at 9 a.m. that five agents are actively running jobs from three concurrent pipelines.

![Concurrent pipelines with additional agents example](_img/concurrent-pipelines-vsts/concurrent-pipelines-with-additional-agents-example.png)

## Determine how many concurrent pipelines you need

You can begin by seeing if your teams can get by with the concurrent pipelines you've got by default. As the number of queued builds and releases exceeds the number of concurrent pipelines you have, your build and release queues will grow longer. When you find the queue delays are too long, you can purchase additional concurrent pipelines as needed.

### Simple estimate

A simple rule of thumb: Estimate that you'll need one concurrent pipeline for every 10 users in your account.

### Detailed estimate

In the following scenarios you might need multiple concurrent pipelines:

* If you have multiple teams, and if each of them require a CI build, then you'll likely need a  concurrent pipeline for each team.

* If your CI build trigger applies to multiple branches, then you'll likely need a concurrent pipeline for each branch.

* If you develop multiple applications using one account or server, then you'll likely need additional concurrent pipelines: one to deploy each application at the same time.

## Purchase additional concurrent pipelines

If you need to more concurrent builds and releases, you can buy concurrent pipelines from the Visual Studio marketplace.

### Private pipelines

If you want to run builds and releases on your own machines (private agents), then [buy private pipelines for build and release](https://marketplace.visualstudio.com/items?itemName=ms.build-release-private-pipelines). After you've done this, you can deploy your own [private agents](../../concepts/agents/agents.md) and use them with these concurrent pipelines.

### Hosted pipelines

If want to run builds and releases on machines on a [hosted agent](../../concepts/agents/hosted.md), then [buy hosted pipelines for build and release](https://marketplace.visualstudio.com/items?itemName=ms.build-release-hosted-pipelines). With the first purchase of a hosted pipeline, the 240 minute limit on total build and release time as well as the 30 minute limit on a single job are waived. Each additional purchase of a hosted pipeline adds another hosted agent for running your builds and releases.

### Sharing of concurrent pipelines among private and hosted agents

No matter which kind of concurrent pipelines you purchase, they are all shared and made available to both private and hosted agents. For example:

0. You purchase a single private pipeline and a single hosted pipeline.

0. You deploy two private agents in a pool.

0. One build and one release are running in your private agent pool.

0. A build is queued in the hosted pool. That build will not start until one of the builds in your private pool is completed.

### Sharing of pipelines across projects in a collection

Pipelines are purchased at the account level, and they are shared amongst all projects in an account. We don't yet offer a way to partition or dedicate certain pipelines to a specific project or agent pool. For example:

0. You purchase two pipelines in your account.

0. You queue two builds in the first project, and both the pipelines are consumed.

0. You queue a build in the second project. That build will not start until one of the builds in your first project is completed.

Builds and releases from all projects are queued and allocated to pipelines in the order they are created. Because of this, it may so happen that a build or a release may wait for a pipeline because of earlier builds waiting for agents. For example:

0. You purchase three pipelines in your account. You have configured two agent pools: A and B, and each contain two agents.

0. You queue three builds targeted for pool A. Two of these builds will start running immediately since you have two agents in pool A. The third has an available pipeline, however it does not have an agent available.

0. You then queue a fourth build targeted for pool B. Since builds are assigned pipelines in the order in which they are created, this build waits for the three builds above to complete, even though there are agents available in pool B.

We're working to improve this model. For now, the workaround is to add more agents to your pool. For example, you could add an agent to pool A mentioned above.

## View available pipelines

0. Browse to **Account settings**, **Build and Release**, **Resource limits**.

 ![control-panel-account-build-and-release-resource-limits](_img/concurrent-pipelines-vsts/control-panel-account-build-and-release-resource-limits.png)

 URL example: `https://{your_account}/_admin/_buildQueue?_a=resourceLimits`

0. View the maximum number of concurrent pipelines that are available in your account.

0. Select **Pipelines queue...** to display all the builds and releases that are actively consuming an available pipeline or that are queued waiting for a pipeline to be available.

## Q&A

### Who can use the Build and Release Management features?

Team Services users with [basic access](https://www.visualstudio.com/products/visual-studio-team-services-feature-matrix-vs) can author as many builds and releases as they want.

To approve releases, basic access is not necessary. Any user with [stakeholder access](../../../work/connect/work-as-a-stakeholder.md) can approve or reject releases.

### I use XAML build controllers with my account. How am I charged for those?

You can register one XAML build controller for each concurrent pipeline in your account. Your account gets one free concurrent pipeline by default, so you can register one XAML build controller for no additional charge. For each additional XAML build controller, you'll need an additional concurrent pipeline.

If you have an account where you run XAML builds using a hosted XAML controller, you should [set up an on-premises build server](https://msdn.microsoft.com/en-us/library/ms181712%28v=vs.120%29.aspx) and switch to an [on-premises build controller](https://msdn.microsoft.com/en-us/library/ee330987%28v=vs.120%29.aspx) now. If you used the hosted XAML build controller, you might have been paying for build minutes, which is a model we no longer support. We will soon block the hosted pool from using the per-minute billing model.

### Why don't I see Visual Studio Enterprise benefits for concurrent pipelines in my Team Services account?

We do offer Visual Studio Enterprise customers some [concurrent pipeline benefits in Team Foundation Server 2017](concurrent-pipelines-tfs.md). We don't yet offer this benefit in Team Services.

### I'm using the Hosted VS2017 or Hosted Linux Preview queue and I'm getting only one agent at a time. Why?

We're offering the **Hosted VS2017** and **Hosted Linux Preview** queues as a preview. So we provide only one of these agents at a time. Eventually we'll offer multiple hosted agents with these capabilities.
