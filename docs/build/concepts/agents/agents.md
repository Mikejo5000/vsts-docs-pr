---
ms.prod: vs-devops-alm
title: Build and Release Agents
description: Build and Release Agents
ms.technology: vs-devops-build
ms.assetid: 5C14A166-CA77-4484-8074-9E0AA060DE58
ms.manager: douge
ms.author: alewis
ms.date: 08/26/2016
---
# Build and Release Agents

**Team Services | TFS 2017 | TFS 2015 | [Previous versions (XAML builds)](https://msdn.microsoft.com/library/dd793166%28v=vs.120%29.aspx)**

To build your code or deploy your software you need at least one agent. As you add more code and people, you'll eventually need more.

When your build or deployment runs, the system begins one or more jobs. An agent is installable software that runs one build or deployment job at a time.

## Hosted agents

If you're using Team Services, you've got the option to build and deploy using a **hosted agent**. When you use a hosted agent, we take care of the maintenance and upgrades. So for many teams this is the simplest way to build and deploy. You can try it first and see if it works for your build or deployment. If not, you can set up a private agent.

> [!NOTE]
> Hosted agents are available only in Team Services, not in Team Foundation Server (TFS).

We provide hosted agents to you in the hosted pool. If you need to run more than one job at a time, you'll need to get more [concurrent pipelines](../licensing/concurrent-pipelines-ts.md).

 [Learn more about hosted agents](hosted.md).

<h2 id="install">Private agents</h2>

An agent that you set up and manage on your own to run build and deployment jobs is a **private agent**. You can use private agents in Team Services or Team Foundation Server (TFS). Private agents give you more control to install dependent software needed for your builds and deployments.

You can install the agent on Windows, Linux, or OSX machines. You can also install an agent on a Linux Docker container.

After you've installed the agent on a machine, you can install any other software on that machine as required by your build or deployment jobs.

### Install and connect to Team Services and TFS 2017

> [!TIP]
> Is your code in Team Services? If so, before you install an agent you might want to see if the hosted pool will work for you. In many cases this is the simplest way to get going. [Give it a try](hosted.md).

* [Windows agent v2](../../actions/agents/v2-windows.md)
* [OSX agent](../../actions/agents/v2-osx.md)
* [Ubuntu 14.04 agent](../../actions/agents/v2-linux.md)
* [Ubuntu 16.04 agent](../../actions/agents/v2-linux.md)
* [RedHat agent](../../actions/agents/v2-linux.md)

### Install and connect to TFS 2015

* [Windows agent v1](../../actions/agents/v1-windows.md)
* [OSX agent](../../actions/agents/v2-osx.md)
* [Ubuntu 14.04 agent](../../actions/agents/v2-linux.md)
* [Ubuntu 16.04 agent](../../actions/agents/v2-linux.md)
* [RedHat agent](../../actions/agents/v2-linux.md)

### Concurrent pipelines for private agents

You might need more concurrent pipelines to use multiple agents at the same time:

* [Concurrent pipelines in Team Services](../licensing/concurrent-pipelines-ts.md)
* [Concurrent pipelines in TFS](../licensing/concurrent-pipelines-tfs.md)

<h2 id="capabilities">Capabilities</h2>

Every agent has a set of capabilities that indicate what it can do. Capabilities are name-value pairs that are either automatically discovered by the agent software, in which case they are called **system capabilities**, or those that you define, in which case they are called **user capabilities**.

The agent software automatically determines various system capabilities such as the name of the machine, type of operating system, and versions of certain software installed on the machine. Also, environment variables defined in the machine automatically appear in the list of system capabilities.

When you author a build or release definition, or when you queue a build or deployment, you specify certain **demands** of the agent. The system sends the job only to agents that have capabilities matching the demands [specified in the definition](../../define/options.md). As a result, agent capabilities allow you to direct builds and deployments to specific agents.

You can view the system capabilities of an agent, and manage its user capabilities by navigating to the **Agent pools** hub and selecting the **Capabilities** tab for the desired agent.

[!INCLUDE [agent-pools-tab](_shared/agent-pools-tab.md)]

> [!TIP]
> 
> After you install new software on a agent, you must restart the agent for the new capability to show up.

<h2 id="communication">Communication</h2>

### Communication with Team Services or TFS

#### Team Services or TFS 2017

The agent communicates with Team Services or TFS to determine which job it needs to run, and to report the logs and job status. This communication is always initiated by the agent. All the messages from the agent to Team Services or TFS happen over HTTP or HTTPS, depending on how you configure the agent. This pull model allows the agent to be configured in different topologies as shown below.

![Agent topologies](_img/agent-topologies.png)

Here is a common communication pattern between the agent and Team Services or TFS.

1. The user registers an agent with Team Services or TFS by adding it to an [agent pool](pools-queues.md). You need to be an [agent pool administrator](pools-queues.md#security) to register an agent in that agent pool. The identity of agent pool administrator is needed only at the time of registration and is not persisted on the agent, nor is used in any further communication between the agent and Team Services or TFS. Once the registration is complete, the agent downloads a _listener OAuth token_ and uses it to listen to the job queue.

2. Periodically, the agent checks to see if a new job request has been posted for it in the job queue in TFS/Team Services. When a job is available, agent downloads the job as well as a _job-specific OAuth token_. This token is generated by TFS/Team Services for the scoped identity [specified in the definition](../../define/options.md). That token is short lived and is used by agent to access (e.g., source code) or modify resources (e.g., upload test results) on Team Services or TFS within that job.

3. Once the job is completed, agent discards the job-specific OAuth token and goes back to checking if there is a new job request using the listener OAuth token.

The communication between the agent and TFS/Team Services is secured using asymmetric encryption over and above HTTPS. Each agent has a public-private key pair, and the public key is exchanged with the server during registration. Server uses the public key to encrypt the payload of the job before sending it to the agent. The agent decrypts the job content using its private key. This is how secrets stored in build definitions, release definitions, or variable groups are secured as they are exchanged with the agent.

#### TFS 2015

In TFS 2015:

* An agent pool administrator joins the agent to an agent pool, and the credentials of the service account (for Windows) or the saved user name and password (for OSX and Linux) are used to initiate communication with TFS. The agent uses these credentials to listening to the job queue.

* The agent does not use asymmetric key encryption while communicating with the server. However, you can [use HTTPS can  to secure the communication](../../../setup-admin/websitesettings.md) between the agent and TFS.

### Communication to deploy to target servers

When you use the agent to deploy artifacts to a set of servers, it must have "line of sight"
connectivity to those servers. The hosted pool, by default, has
connectivity to Windows Azure websites and Windows servers running in Azure.

If your on-premises environments do not have connectivity to the hosted pool
(which is typically the case due to intermediate firewalls), you'll need to
manually configure a private agent on on-premises computer(s). The agents must have connectivity to the target
on-premises environments, and access to the Internet to connect to Team Services or Team Foundation Server,
as shown in the following schematic.

![Agent connectivity for on-premises environments](_img/agent-connections.png)

## Authentication

To register an agent, you need to be a member of the [administrator role](pools-queues.md#security) in the agent pool. Your agent can authenticate to Team Services or TFS using one of the following methods:

* **Personal Access Token (PAT):** [Generate](../../../setup-admin/team-services/use-personal-access-tokens-to-authenticate.md) and use a PAT to connect an agent with Team Services, TFS 2017, or TFS 2015 Update 3. PAT is the only scheme that works with Team Services.

* **Integrated:** Connect a Windows agent to TFS using the credentials of the signed-in user via a Windows authentication scheme such as NTLM or Kerberos.

* **Negotiate:** Connect to TFS as a user other than the signed-in user via a Windows authentication scheme such as NTLM or Kerberos.

* **Alternate:** Connect to TFS using Basic authentication. To use this method you'll first need to [configure HTTPS on TFS](../../../setup-admin/websitesettings.md).

<h2 id="account">Interactive vs. service</h2>

You can run your agent as either a service or an interactive process. After you've configured the agent, we recommend that you first try it in interactive mode to make sure it works. Also, in some cases you might need to run the agent interactively for production use. For example, if you need to run an elevated process or run UI tests.

After you've verified that the agent is working, for production use, we recommend that you run the agent as a service. The main advantage is that the agent stays more reliably in a running state. For example, it starts automatically when you restart the machine and after some kinds of failures. You can leverage the service manager of the operating system to manage the life cycle of the agent. Also, the experiences for auto-upgrading agents are better when they are run as services.

Whether you run an agent as a service or interactively, you can choose which account you use to run the agent. Note that this is different from the credentials that you use when you register the agent with Team Services or TFS. The choice of agent account depends solely on the needs of the tasks running in your build and deployment jobs. For instance, to  run tasks that use Windows authentication to access an external service, you need to run the agent using an account that has access to that service.

## Agent version and upgrades

We update the agent software every few weeks in Team Services, and with every update in TFS. We indicate the agent version in the format `{major}.{minor}`. For instance, if the agent version is `2.1`, then the major version is 2 and the minor version is 1. When a newer version of the agent is only different in minor version, it is automatically upgraded by Team Services or TFS. This upgrade happens when one of the tasks requires a newer version of the agent.

If you run the agent interactively, or if there is a newer major version of the agent available, then you have to manually upgrade the agents. You can do this easily from the agent pools tab under your team project collection or account.

You can view the version of an agent by navigating to the **Agent pools** hub and selecting the **Capabilities** tab for the desired agent.

[!INCLUDE [agent-pools-tab](_shared/agent-pools-tab.md)]

## Q&A

### Can I install multiple private agents on the same machine?

Yes. This approach can work well for agents that run jobs that don't consume a lot of shared resources. For example, you could try it for agents that run releases that mostly orchestrate deployments and don't do a lot of work on the agent itself.

You might find that in other cases you don't gain much efficiency by running multiple agents on the same machine. For example, it might not be worthwhile for agents that run builds that consume a lot of disk and I/O resources. 

You might also run into problems if concurrent build processes are using the same singleton tool deployment, such as NPM packages. For example, one build might update a dependency while another build is in the middle of using it, which could cause unreliable results and errors.

[!INCLUDE [agent-latest-version](_shared/v2/qa-agent-version.md)]
