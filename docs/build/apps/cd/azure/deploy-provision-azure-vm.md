---
ms.assetid: 10C708EC-0D2A-4EF8-9381-4CF8B1EBA755
title: Provision an Azure Virtual Machine using Azure RM templates with Microsoft Release Management in Visual Team Services and Team Foundation Server
description: Provision a Microsoft Azure Virtual Machine using Azure Resource Manager templates in Microsoft Release Management in Visual Team Services (VSTS) and Team Foundation Server (TFS)
ms.prod: vs-devops-alm
ms.technology: vs-devops-release
ms.manager: douge
ms.author: ahomer
ms.date: 10/20/2016
---

# Provision an Azure virtual machine using an Azure RM template

[!INCLUDE [version-rm-dev14](../../../_shared/version-rm-dev14.md)]

In just a few steps, you can provision Azure virtual machines (VMs)
using [Resource Manager (RM) templates](https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/).
Managing the definitions for virtual machines in this
way is considered **Infrastructure as code** and is
a good DevOps practice.

## Get set up

### Begin with a CI build

Before you begin, you need a CI build that creates your Azure RM template. To set up CI, see:

* [Build an Azure virtual machine using an Azure RM template](build-azure-vm-template.md)

## Create an Azure RM connection

Follow these steps to establish a connection from Team
Foundation Server or Visual Studio Team Services to
Azure. You need an Azure subscription.

1. Open your Team Services or TFS team project in 
   a web browser. Choose the **Settings** icon in the menu bar and select **Services**.

1. In the **Services** tab, choose **New Service Endpoint** 
   and select **Azure Resource Manager**.

1. Enter a user-friendly name for the connection and select your Azure subscription.
 
   >If the subscription you require is not shown in the service endpoint dialog, see
   [Azure Resource Manager service endpoint](../../../concepts/library/service-endpoints.md#sep-azure-rm-conditions)
   for more information and 
   [Troubleshoot Azure Resource Manager service endpoints](../../../actions/azure-rm-endpoint.md).

   Or, if you prefer to use an existing service principal,
   use the link near the bottom to open the full version of
   the dialog and follow these steps:

   - Download and run **[this PowerShell script](https://github.com/Microsoft/vsts-rm-documentation/blob/master/Azure/SPNCreation.ps1)** in an Azure PowerShell window. 
   - Enter a user-friendly name for the connection.
   - Copy these fields from the output of the PowerShell script into the Azure subscription dialog textboxes:
     * Subscription ID
     * Subscription Name
     * Service Principal ID
     * Service Principal Key
     * Tenant ID<p/>
 
1. Choose **OK** to save the Azure service endpoint.

## Create the release definition

Carry out the following steps to deploy the Azure Resource Group.

1. Open the **Releases** tab of the **Build &amp; Release** hub and choose the
   "**+**" icon to create a new release definition.

1. In the **Create release definition** dialog, select the **Empty** template and choose **Next**.

1. In the next page, select the build definition you created 
   earlier and choose **Create**. This creates a new release definition 
   with one default environment.

1. In the new release definition, select **+ Add tasks** and add an **Azure Resource Group Deployment** task.
   Optionally edit the name to help identify the task, such as **Provision Windows 2012 R2 VM**.

1. Configure the **Azure Resource Group Deployment** task as follows:

   | Task step | Parameters |
   | --------- | ---------- |
   | ![Azure Resource Group Deployment](../../../steps/deploy/_img/azure-resource-group-deployment-icon.png)<br/>[Deploy: Azure Resource Group Deployment](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/AzureResourceGroupDeployment)<br/>Deploy files to an Azure Resource Group. | **Azure Subscription**: Select the name of the Azure Resource Manager endpoint you defined earlier.<br/>**Action**: `Create or Update Resource Group`.<br/>**Resource Group**: Enter a name for a new resource group, or specify an existing resource group.<br/>**Template location**: The path of the Resource Manager template; for example: `$(System.DefaultWorkingDirectory)\ASPNet4.CI\drop\HelloWorldARM\Templates\WindowsVirtualMachine.json`.<br/>**Template Parameters**: The path of the Resource Manager template parameters file; for example `$(System.DefaultWorkingDirectory)\ASPNet4.CI\drop\HelloWorldARM\Templates\WindowsVirtualMachine.parameters.json`.<br/>**Override Template Parameters**: A list of values for the parameters in the template; for example: `-adminUsername $(vmuser) -adminPassword (ConvertTo-SecureString -String $(vmpassword) -AsPlainText -Force) -dnsNameForPublicIP $(dns)'`.<br/>**Enable Deployment Prerequisites**: Checked.<br/>**Output - Resource Group**: The name of the Resource Group output from the task as a value that can be used as an input to further deployment tasks. |
   
   >Checking the **Enable Deployment Prerequisites** checkbox
   configures WinRM on the virtual machine and enables
   execution of remote PowerShell scripts, which may be
   required to deploy an application. Also notice the use of
   **ConvertTo-SecureString** to specify the value for **adminPassword**.
   You must do this because **adminPassword** is defined as a **SecureString**
   type in the Resource Manager template file.

1. If you used variables in the parameters of the **Azure Resource Group Deployment** task,
   such as **vmuser**, **vmpassword**, and **dns**, set the values for them in the
   environment configuration variables. Encrypt the value
   of **vmpassword** by selecting the "padlock" icon.

1. Enter a name for the release definition and save it.

1. Create a new release, select the latest build, and 
   deploy it to the single environment.

## Q&A

<!-- BEGINSECTION class="md-qanda" -->

[!INCLUDE [temp](../../../_shared/qa-versions.md)]

<!-- ENDSECTION -->

[!INCLUDE [rm-help-support-shared](../../../_shared/rm-help-support-shared.md)]

