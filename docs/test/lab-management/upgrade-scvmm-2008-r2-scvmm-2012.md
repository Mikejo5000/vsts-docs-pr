---
title: Upgrade SCVMM 2008 R2 to SCVMM 2012 | Team Foundation Server
description: Upgrade SCVMM 2008 R2 to SCVMM 2012
ms.technology: vs-devops-test-continuous 
ms.prod: vs-devops-alm
ms.assetid: 5be92444-c701-43c7-8b2a-77df8e02bc27
ms.manager: douge
ms.author: ahomer
ms.date: 08/12/2016
---

# Upgrade SCVMM 2008 R2 to SCVMM 2012

**Visual Studio 2017** | **Visual Studio 2015** | [**Previous version**](https://msdn.microsoft.com/library/hh757363%28v=vs.120%29.aspx)

Lab Management for Team Foundation Server supports 
SCVMM 2008 R2 and SCVMM 2012. If you are upgrading 
Team Foundation Server 2013 to Team Foundation 
Server 2015, and plan to upgrade SCVMM 2008 R2 to 
SCVMM 2012, we recommend that you upgrade to SCVMM 
2012 after you complete your upgrade to Team 
Foundation Server 2015. This topic describes how 
to upgrade SCVMM 2008 R2 to SCVMM 2012 when you are 
using Lab Management on Team Foundation Server 2015.
Lab Management **does not** support SCVMM 2016. 

**Important:**  When you upgrade SCVMM, certain 
steps will cause some downtime for your Team 
Foundation Server. You'll find these steps below.

## Upgrading to SCVMM 2012

1. Use the SCVMM 2012 installer to upgrade SCVMM 
   2008 R2 Server to SCVMM 2012 Server.

1. Upgrade the SCVMM agents on your hosts and 
   library shares.

1. Use the SCVMM Administration Console to verify 
   that all of your SCVMM components are working.

1. Install SCVMM 2012 Administration Console on 
   all machines of the application tier of your Team 
   Foundation Server.

1. Use the **iisreset** command to restart the 
   Team Foundation Server web service. Then restart 
   the Team Foundation Server job agent.

   **Caution:** This step will disrupt the services 
   on your Team Foundation Server.

1. Upgrade the data and templates in each project 
   collection database so it is compatible with SCVMM 
   2012.

   Open an elevated command prompt on your Team 
   Foundation Server and enter the following command:

   **C:\\Program Files\\Microsoft Team Foundation 
   Server 14.0\\Tools\> tfsconfig lab /upgradeSCVMM /collectionName:\***

   When you use the **upgradeSCVMM** command, Team 
   Foundation Server will create a new template object 
   on your SCVMM server for every team project that 
   uses that template. This ensures that your templates
   are upgraded to be compatible with SCVMM 2012 
   without losing any data. However, when the new 
   templates are created, the team project name is 
   appended to the template name.

   **Caution:**  
   If the new template name is greater than 64 
   characters, this will cause an SCVMM failure. To 
   resolve this error, you must give those templates a 
   shorter name. If you encounter any other errors or 
   warnings when you run this command, see the next 
   section to resolve those errors. If you do not 
   encounter any errors or warnings, your upgrade is 
   complete and you can begin using SCVMM environments 
   with Lab Management.

## Resolving errors and warnings when using the upgradeSCVMM command

After you use the **upgradeSCVMM** command, you 
must resolve any errors or warnings you receive 
then rerun the command before you can start using 
Lab Management. The **upgradeSCVMM** command 
generates a log file that contains information 
about any errors and warnings that you encounter. 
The location of the log file is displayed when you 
run the **upgradeSCVMM** command.

**SCVMM failure:** If you receive an error that is 
related to an SCVMM failure, use your SCVMM job 
history to get additional information about the 
error. After you resolve the error in SCVMM, rerun 
the **upgradeSCVMM** command.

## See also

* [Change Existing Lab Management Configurations](https://msdn.microsoft.com/library/ee704508%28v=vs.140%29.aspx)
* [Test apps early and often](../index.md)

[!INCLUDE [help-and-support-footer](../_shared/help-and-support-footer.md)] 
