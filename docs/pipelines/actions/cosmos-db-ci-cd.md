---
title: CI/CD with APP Service and Azure Cosmos DB | VSTS Tutorial
description: Use VSTS to enable Continuous Integration (CI) and Continous Deployment (CD) for your Azure Cosmos DB.
ms.author: mlearned
ms.manager: douge
ms.prod: devops
ms.technology: devops-cicd
ms.topic: tutorial
ms.date: 08/01/2018
author: mlearned
monikerRange: 'vsts'
---


# Tutorial:  CI/CD with App Service and Azure Cosmos DB

Create a continuous integration (CI) and continuous delivery (CD) pipeline for Azure Comsos DB backed Azure App Service Web App.  Azure Cosmos DB is Microsoft’s globally distributed, multi-model database. Cosmos DB enables you to elastically and independently scale throughput and storage across any number of Azure’s geographic regions. 

You will:

> [!div class="checklist"]
> * Clone a sample Azure Web App to your VSTS repository
> * Create a Cosmos DB collection and database
> * Set up CI for your app
> * Set up CD to Azure for your app
> * Test the CI/CD pipeline

## Prerequisites

* An Azure subscription. You can get one free through [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/).
* A VSTS organization. If you don't have one, you can [create one for free](https://go.microsoft.com/fwlink/?LinkId=307137). If your team already has one, then make sure you are an administrator of the project you want to use.

## Clone a sample Azure Web App to your VSTS repository

This sample shows you how to use the Microsoft Azure Cosmos DB service to store and access data from an ASP.NET MVC application hosted on Azure Websites.

To import the sample app into a Git repo in VSTS:

 <TODO INSERT SIGN IN STEPS>

 1. On the **Code** hub for your project in VSTS, select the drop down and choose the option to **Import repository**.

 1. In the **Import a Git repository** dialog box, paste https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git into the **Clone URL** text box.

 1. Click **Import** to copy the sample code into your Git repo.

## Set up CI for your App

1. On the build and release hub for your project in VSTS, select **builds**.

1. On the right-side of the screen, select **+ NEW** to create a new build.

1. Choose the **repository** for the sample application you imported earlier in this tutorial, and then cnoose **continue**.

1. Search for the **ASP.NET Application** build template, and then select **Apply**.

1. Select the **triggers**, and then select the checkbox for ""Enable cotinuous integration**.  This setting ensures every commit to the repository excecutes a build.

1. Select **Save & Queue**, and then choose **Save and Queue** to execute a new build.

1. Select the build **hyperlink** to examine the running build.  In a few minutes the build completes.  The build produces artifacts which can be used to deploy to Azure.

## Set up CD to Azure for your App

The CI for the sample app produces the artifacts needed for deployment to Azure.

1. Select **Release** to create a release definition linked to the build artifacts from the CI pipeline you created with the previous steps.

1. Choose the **Azure App Service deployment** template, and then choose **Apply**.

1. On the **Environments** section, select the **1 phase and 1 task** link.

1. Select the **Azure Subscription**  <TODO ENDPOINT STUFF>

1. Choose an **App Service name**.

1. Select the **Deploy Azure App Service** task, and then select the **File Transforms & Variable Substitution Options** setting.  

1. Enable the checkbox for **XML Variable substitution**.

1. At the top of the menu, select **Variables**.

1. Select **+ Add** to create a new variable named **endpoint**.  Select **+ Add** to create a second variable named **authKey**.

1. Select the **padlock** icon to make the authKey variable secret.

1. Select the **Pipeline** menu.

1. Under the **Artifacts** ideas, choose the **Continuous deployment trigger** icon.  On the right side of the screen, ensure **Enabled** is on.

1. Select **Save** to save changes for the release defintion.

<TODO need the values for cosmos>

## Test the CI/CD pipeline
<TODO>

## Clean up resources

 > [!NOTE]
 > The steps below will permanently delete resources.  Only use this functionality after carefully reading the prompts.

<TODO DO CLEANUP>

## Next steps

You can optionally modify these build and release definitions to meet the needs of your team. You can also use this CI/CD pattern as a template for your other projects.  You learned how to:

> [!div class="checklist"]
> * Clone a sample Azure Web App to your VSTS repository
> * Create a Cosmos DB collection and database
> * Set up CI for your app
> * Set up CD to Azure for your app
> * Test the CI/CD pipeline


To learn more about the VSTS pipeline see this tutorial:

> [!div class="nextstepaction"]
> [Customize CD process](../release/define-multistage-release-process.md)
