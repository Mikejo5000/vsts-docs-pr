---
title: Deployment groups in Release Management
description: Deployment Groups for Release Management on Visual Studio Team Services (VSTS) and Team Foundation Server (TFS)
ms.assetid: 21416B0A-F60F-436F-AB46-D6C2A54D5707
ms.prod: vs-devops-alm
ms.technology: vs-devops-release
ms.manager: douge
ms.author: ahomer
ms.date: 05/12/2017
---

# Deployment groups

**| Team Services |**

>**Team Services:** Deployment groups are not yet available to all Team Services accounts.
>**TFS:** At present, deployment groups are not available in Team Foundation Server.

A deployment group is a logical set of deployment target machines 
that have agents installed on each one. Deployment Groups represent the physical environments;
for example, "Dev", "Test", "UAT", and "Production".

When authoring a Team Services or TFS Release definition, you
can specify the deployment targets for a [phase](../../../process/phases.md)
using a deployment group. This makes it easy to define
[parallel execution](../../../process/phases.md#parallelexec)
of deployment tasks.

Deployment groups:

* Specify the security context and runtime
  targets for the agents. As you create a deployment group, you
  add users and give them appropriate permissions to administer,
  manage, view, and use the group.

* Let you view live logs for each server as a
  deployment takes place, and download logs for all servers to
  track your deployments down to individual machines.

* Enable you to use machine tags to limit deployment to specific
  sets of target servers.

## Create a deployment group

You define groups on the **Deployment Groups** tab of the **Build &amp; Release** hub.
When you create a new deployment group, you specify the name and description.
The **Details** page generates a script that you must execute on each of your target servers
to install and prepare the agent.

![Creating a deployment group](_img/index/depgroup-create.png)

## Manage deployment groups

After you prepare your target servers, they appear in the **Machines** tab.
The list indicates if a server is available, the tags you assigned to each server,
and the latest deployment. Select a server to see an overview, manage the
machine tags, or remove the server from the deployment group.

![Overview of a deployment group](_img/index/depgroup-02.png)

> Notice how the tags assigned in the example above will allow deployment to
  on-premises servers, cloud-hosted servers, or specific servers when 
  the deployment group is used in a [**Run on machine group** phase](../../../process/phases.md#deployment-group-phase).

Use the **...** icon for a server to perform actions such as displaying
details, or deleting the machine. 

![Delete a deployment group](_img/index/depgroup-05.png)

Manage the security for a deployment group by assigning security roles.
 
![Security for a deployment group](_img/index/depgroup-04.png)

View the capabilities for the agent installed on each server.

![Capabilities of a deployment group](_img/index/depgroup-03.png)

## Monitor releases for deployment groups

When release is executing, you see an entry in the
[live logs page](../../../../actions/debug-deployment-issues.md)
for each server in the deployment group. After a release has completed,
you can download the log files for every server to examine the deployments
and resolve issues. To navigate quickly to a release definition or a release,
use the links in the **Releases** tab. 

![Viewing releases for a deployment group](_img/index/depgroup-01.png)

## Related topics

* [Run on machine group phase](../../../process/phases.md#deployment-group-phase)
* [View and manage releases](../../../../actions/view-manage-releases.md)
* [Monitor releases and debug deployment issues](../../../../actions/debug-deployment-issues.md)
* [Deploy an agent on Windows](../../../../actions/agents/v2-windows.md)
* [Deploy an agent on OSX](../../../../actions/agents/v2-osx.md)
* [Deploy an agent on Linux](../../../../actions/agents/v2-linux.md)

[!INCLUDE [rm-help-support-shared](../../../../_shared/rm-help-support-shared.md)]

