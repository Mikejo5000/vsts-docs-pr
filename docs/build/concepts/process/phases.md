---
title: Build and Release Automation Phases in Visual Studio Team Services and Team Foundation Server
description: Understand Build and Release Phases in Visual Studio Team Services (VSTS) and Team Foundation Server (TFS)
ms.assetid: B05BCE88-73BA-463E-B35E-B54787631B3F
ms.prod: vs-devops-alm
ms.technology: vs-devops-release
ms.topic: get-started-article
ms.manager: douge
ms.author: ahomer
ms.date: 10/20/2016
---

# Phases in Build and Release Management

**TFS 2017 | Team Services**

Tasks can run in different **phases**, which effectively represent different execution locations.

By using different task phases in a build or release definition, you can:

* Specify sets of tasks that will run on a specific agent or on the server,
  and use different agent queues and agents for the tasks in separate phases.

* Introduce a manual intervention task where deployment pauses while an
  operator carries out manual processes or validates the state of the system
  before continuing the deployment.

* Switch off downloading of artifacts for sets of tasks that include
  their own logic for accessing source artifacts, or that do not require access
  to artifacts. This can reduce execution time and improve deployment efficiency.

* Permit access to OAuth tokens for only the tasks that need to interact
  with Team Services or Team Foundation Server.  

* Specify different execution timeouts for different sets of tasks to
  maximize deployment performance and control.

  ![Task phases schematic diagram](_img/phases-01.png)

The task phases you can use are:

* **[Agent phase](#agent-phase)**. In this phase, tasks are executed on the computer(s) that host the build and release agent.

* **[Server phase](#server-phase)**. In this phase, tasks are orchestrated by and executed on the Team Services
  or Team Foundation Server. A server phase does not require an agent
  or any target computers.

* **[Deployment group phase](#deployment-group-phase)**. In this phase, tasks are executed on the computer(s) defined in a
  [deployment group](../definitions/release/deployment-groups/index.md),
  each of which hosts the build and release agent.

By default, tasks you add to a build definition or release definition run in a single default agent phase.
To add tasks to a specific phase when you have more than one phase in the definition, select the target phase
and then choose **+ Add tasks**.

> **TFS 2015**: Features explained in this article are not available in TFS 2015.

## Agent phase

An **agent phase** is a way of defining a sequence of tasks that will run on one or more agents.
At run time, one or more jobs are created to be run on agents that match the demands specified in the phase properties.

![Specifying agent phase properties](_img/phases-03.png)

You can configure the following properties for an agent phase:

* **Deployment queue:** Use this option to specify the agent queue
  in which the jobs will run. In the case where multiple jobs are created, all the jobs run on agents within the same agent queue.

* **Demands:** Use these settings to specify how an agent for
  executing the tasks will be selected. In the case where multiple jobs are created, all the agents must satisfy the demands.

* **Run on multiple agents in parallel:** If you have installed
  multiple agents, you can specify how the tasks will run in parallel
  on these agents. Select **Multi-agent** and specify the number
  of agents to use, or select **Multi-configuration** and specify
  details of the multipliers to use. See [parallel execution using agent phases](#parallelexec).

* **Timeout:** Use this option if you
  want to specify the timeout in minutes for jobs in this phase. A zero
  value for this option means that the timeout is effectively
  infinite and so, by default, jobs run until they complete or fail.
  You can also set the timeout for each task individually -
  see [task control options](tasks.md#controloptions).

* **Skip artifacts download:** When used in a release definition, you may choose to skip the
  [download of artifacts](../definitions/release/artifacts.md#download)
  during the job execution. Use this option if you want to implement
  your own custom logic for downloading artifacts by using tasks, or if the tasks in a particular phase do not rely on the artifacts.

* **Allow scripts to access OAuth token:** Use this option if you
  want to allow tasks running in this phase access to the
  current Team Services or TFS OAuth security token.
  This is useful in many scenarios, such as when you need to
  run a custom PowerShell script that invokes the REST APIs
  on Team Services - perhaps to create a work item or query a build for information.

<a name="parallelexec"></a>
### Parallel execution using agent phases

You can use multiple agents to run parallel jobs if you configure an agent phase to be **Multi-configuration** or **Multi-agent**. Here are some examples where **Multi-configuration** execution is appropriate:

* **Multi-configuration builds:** An agent phase can be used in a 
  build definition to build multiple configurations in parallel. For 
  example, you could build a C++ app for both debug and release 
  configurations on both x86 and x64 platforms. To run multiple jobs,
  you identify a variable named a **multiplier**, and specify a list
  of values for that multiplier. A separate job is run for each value
  in the list. For example, you can run two parallel jobs if you 
  define a variable named **BuildConfiguration** with the value
  `Debug,Release` and specify that variable to be used as a
  multiplier in the build definition. When you identify two variables
  to act as a multiplier, each with two values, you effectively
  create four jobs, one for each combination of values of the two
  variables. For more details and an example of multi-configuration
  build, see [Visual Studio Build](../../steps/build/visual-studio-build.md).

* **Multi-configuration deployments:** An agent phase can be used
  in an environment of a release definition to run multiple deployment
  jobs in parallel. For example, to configure your application to be
  load balanced across a site in US and a site in Europe, you can
  define a variable named **Location** with the value `US,Europe`,
  and specify that variable to be used as a multiplier in the agent
  phase of the environment. If two agents are available, both the
  jobs will be run simultaneously - one with **Location = US**, and
  another with **Location = Europe**. If only one agent is available,
  the first job is run, followed by the second job. When a multiplier
  results in many jobs being created in parallel, you can also specify
  the maximum number of agents that can be used for parallelism. For
  example, if **Location** has ten values, you can restrict to five
  sites being deployed in parallel by specifying **5** for the
  maximum number of agents.

  > Multi-configuration deployments are not possible with Release Management in TFS 2015.

* **Multi-configuration testing:** An agent phase can be used in an
  environment of a release definition to run a set of tests in
  parallel - once for each test configuration. For example, to run a
  suite of web tests, once for each browser, you can define a variable
  named **Browser** with the value `IE,Chrome,Edge,Firefox` and
  specify that variable to be used as a multiplier. As the agent
  demands are specified only once for an agent phase, all agents
  should be pre-installed with all the browsers. As with multi-configuration
  deployment, you can specify the maximum number of agents that can
  be used at the same time for multi-configuration testing.

  > Multi-configuration testing is only possible with Release definitions in TFS 2017 and Team Services. It is not possible with Build definitions.

To use the **Multi-configuration** option for deployment, you must:

* Define one or more [variables](../definitions/release/variables.md)
  on the **Variables** tab of the definition (or in a 
  [variable group](../library/variable-groups.md)).
  Each variable, known in this context as a _multiplier_ variable,
  must be defined as a comma-delimited list of the values you want
  to pass individualy to the agents. 

* Enter the name of the multiplier variable, without the **$** and parentheses, as the
  value of the **Multipliers** parameter. 

* If you want to execute the phase for more than one multiplier variable, enter
  the variable names as a comma-delimited list - omitting the **$** and parentheses
  for each one.

* If you want to limit the number of agents used during the deployment to a
  number less than you have configured for your account, enter that value as the
  **Maximum number of agents** parameter.

For example, you might define two variables named **Location** and **Browser** as follows::

* **Location** = `US,Europe`
* **Browser** = `IE,Chrome,Edge,Firefox`

The following configuration will execute the deployment eight times using 
a maximum of four agents at any one time:

* **Multipliers** = `Location,Browser`
* **Maximum number of agents** = `4`

![Configuring multi-configuration execution](_img/phases-04.png)

## Server phase

Use a server phase in a release definition to run tasks that do
not require an agent, and execute entirely on the Team Services or Team Foundation Server. Only one task, **Manual Intervention**, is supported in a server phase at present.

> Server phases and manual intervention tasks only work in release definitions in Team Services and TFS 2017.

### The Manual Intervention task

The **Manual Intervention** task does not perform
deployment actions directly. Instead, it allows you to
pause an active deployment within an environment, typically to perform some
manual steps or actions, and then continue the automated deployment steps.

The **Manual Intervention** task configuration includes an **Instructions** parameter that
can be used to provide related information, or to specify the manual steps
the user should execute during the server phase. You can configure the task to
send email notifications to users and user groups when it is awaiting intervention,
and specify the automatic response (reject or resume the deployment) after a configurable
timeout occurs.

When the Manual Intervention task is activated during a deployment, it sets
the deployment state to **IN PROGRESS** and displays
a message bar containing  a link that opens the
Manual Intervention dialog containing the instructions.
After carrying out the manual steps, the administrator
or user can choose to resume the deployment, or reject it. Users with **Manage deployment** permission on the environment can resume or reject the manual intervention.

## Deployment group phase

Deployment groups make it easy to define groups of target servers for deployment,
and install the required agent on each one. Tasks that you define in a
deployment group phase run on some or all of the target servers, depending on
the arguments you specify for the tasks and the phase itself.

![Dependency group properties](_img/depgroup-properties.png)

You can select specific sets of servers from a deployment group to receive
the deployment by specifying the machine tags that you have defined for each
server in the deployment group. For more details, see [Deployment groups](../definitions/release/deployment-groups/index.md).

You can also specify the proportion of the target servers that the process should
deploy to at the same time - such as half the servers, all the servers, or
a custom setting. This ensures that the app running on these servers is 
capable of handling requests while the deployment is taking place. 

![Dependency group properties](_img/depgroup-deployto.png)

## Multiple phases

You can add multiple phases to a release definition, and then add
tasks to each one by selecting the target phase for the new tasks.

> Multiple phases can only be used in Release Management in Team Services and TFS 2017.

For example, the definition shown below divides the overall release
execution into separate execution phases by using two agent phases
and a server phase.

![Configuring a manual intervention step](_img/phases-02.png)

In the example above:

1. The tasks in the first phase of the release run on an agent
   and, after this phase is complete, the agent is released.

1. The server phase contains a Manual Intervention task
   that runs on the Team Services or Team Foundation Server.
   It does not execute on, or require, an agent or any target servers.
   The Manual Intervention task displays its message and waits for a
   "resume" or "reject" response from the user. In this example, if
   the configured timeout of 360 minutes is reached, the task will
   automatically reject the deployment (set the timeout to zero if
   you do not want an automated response to be generated).   

1. If the release is resumed, tasks in the third phase run -
   possibly on a different agent. If the release is rejected,
   this phase does not run and the release is marked as failed.

It's important to understand some of the consequences of
phased execution:

* The artifacts are downloaded to the agent at the start of
  every agent phase because these phases may use different
  agents. You should not assume that the state from an earlier
  phase is available during subsequent phases.

* The **Continue on Error** and **Always run** options for
  tasks in each phase do not have any effect on tasks in
  subsequent phases of the release. For example, setting
  **Always run** on a task at the end of the first phase will
  not guarantee that tasks in subsequent phases will run.

## Related topics

* [Tasks](tasks.md)
* [Task groups](../library/task-groups.md)

[!INCLUDE [rm-help-support-shared](../../_shared/rm-help-support-shared.md)]
