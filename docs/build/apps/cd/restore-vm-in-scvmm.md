---
ms.assetid: CA18DBF9-3495-47CD-B1C8-E20705D09309
title: Restore a virtual machine using System Center Virtual Machine Manager (SCVMM) from Release Management in Visual Studio Team Services or Microsoft Team Foundation Server
description: Example of restoring a virtual machine in System Center Virtual Machine Manager (SCVMM) to a clean snapshot from Release Management in Visual Studio Team Services (VSTS) or Microsoft Team Foundation Server (TFS)
ms.prod: vs-devops-alm
ms.technology: vs-devops-release
ms.manager: douge
ms.author: ahomer
ms.date: 10/20/2016
---

# Restore a virtual machine using System Center Virtual Machine Manager

[!INCLUDE [version-rm-dev14](../../_shared/version-rm-dev14.md)]

This example shows how you can integrate **System 
Center Virtual Machine Manager** (SCVMM) with Release Management in 
Visual Studio Team Services or Team Foundation Server. You can restore 
virtual machines managed by SCVMM to a clean snapshot and 
then deploy your apps to them.

## Prepare

You will need a minimum of two machines - a **target server** 
or virtual machine to deploy to, and an **agent machine** that 
drives the deployment. You may have multiple target 
servers depending on how many nodes you want to 
deploy to. However, you only need one agent 
machine to drive the deployment.

1. Install the System Center Virtual Machine Manager (SCVMM) extension
   from Visual Studio Marketplace into your server or account.

   * If you are using **Visual Studio Team Services**,
     install the extension from [this location](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.scvmmapp)
     in Visual Studio Marketplace.
   * If you are using **Team Foundation Server**, download
     the extension from [this location](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.scvmmapp)
     in Visual Studio Marketplace, upload it to your
     Team Foundation Server, and install it.<p />

1. Install an agent on the **agent machine**:

   * [Deploy an agent on Windows](../../actions/agents/v2-windows.md)
   * [Deploy an agent on OSX](../../actions/agents/v2-osx.md)
   * [Deploy an agent on Linux](../../actions/agents/v2-linux.md)<p />

1. Install the **Virtual Machine Manager** (VMM) console by
   following [these instructions](https://technet.microsoft.com/library/gg610627.aspx).
   Supported version: [System Center 2012 R2 Virtual Machine Manager](https://technet.microsoft.com/library/hh546785.aspx).

1. Create an SCVMM service endpoint in your team project:

   * Open your Team Services or TFS team project in 
     your web browser. Choose the **Settings** icon in the menu bar and select **Services**.

   * In the **Services** tab, choose **New Service Endpoint**, and select **SCVMM**.

   * In the **Add new SCVMM Connection** 
     dialog, enter the values required to connect to the 
     SCVMM Server:

     - **Connection Name**: Enter a user-friendly name 
       for the service endpoint such as **MySCVMMServer**.
     - **SCVMM Server Name**: Enter the fully qualified domain 
       name and port number of the SCVMM server, in the form **machine.domain.com:port**.
     - **Username** and **Password**: Enter the credentials
       required to connect to the vCenter Server. Username formats such as **username**, **domain\username**,
       **machine-name\\username**, and **.\\username** are supported.
       UPN formats such as **username@domain.com** and built-in system 
       accounts such as **NT Authority\\System** are not supported.<p />

1. Choose **OK** to save the settings and create the connection.

## Deploy

1. Open the **Releases** tab of the **Build &amp; Release** hub and choose the
   "**+**" icon to create a new release definition.

1. In the **Create release definition** dialog, 
   select the **Empty** template and choose **Next**.

1. In the next page, select **Choose Later** and then choose **Create**.
   This creates a new release definition with one 
   default environment and no linked artifacts.

1. Choose **+ Add tasks** and add an **SCVMM** task 
   from the **Deploy** section of the **Task catalog** 
   dialog to the environment.

1. To configure the **SCVMM** task to restore a 
   virtual machine that is already managed in SCVMM to 
   a snapshot, use the following settings:

   | Task step | Parameters |
   | --------- | ---------- |
   | ![SCVMM](_img/scvmm/scvmm-icon.png)<br/>[SCVMM](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.scvmmapp)<br/>Connect to a SCVMM server and perform actions on Virtual Machine(s). | **SCVMM Service Connection**: Select the SCVMM connection you created earlier.<br/>**Action**: `Restore Checkpoint`<br/>**Virtual Machine Names**: Enter the names of one or more **target** virtual machines. Separate multiple names with a comma; for example, `fabrikamdev,fabrikamqa,prod05`<br/>**Checkpoint Name**: Enter the name of the checkpoint that will be applied to the virtual machines. This checkpoint must exist.<br/>**Select VMs from**: Optional. You can specify a filter to scope the source for virtual machines to either `CLOUD` or `HOST`. Leave it set to `None` |

1. You can now add other tasks to the environment, 
   such as **PowerShell on Target Machines** and then 
   deploy to the newly provisioned machines.

   > In the future we plan for the **SCVMM** task 
   to provide an output variable that you
   set in the task and then use as input to subsequent
   tasks. Until then, if you want to run additional tasks, 
   you'll need to specify the fully-qualified domain 
   names of the virtual machines that are provisioned 
   in SCVMM.

1. Type a name for the new release definition and save it.

1. Create a new release from the release definition
   and deploy it to the environment.

## Q&A

<!-- BEGINSECTION class="md-qanda" -->

[!INCLUDE [temp](../../_shared/qa-versions.md)]

<!-- ENDSECTION -->

[!INCLUDE [rm-help-support-shared](../../_shared/rm-help-support-shared.md)]
