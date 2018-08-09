---
title: Azure SQL database deployment
description: Deploy to an Azure SQL database from VSTS or TFS
ms.prod: devops
ms.technology: devops-cicd
ms.topic: conceptual
ms.manager: douge
ms.author: glenga
author: ggailey777
ms.date: 08/09/2018
---

# Azure Functions deployment

[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview) enables you to execute your code in a [serverless](https://azure.microsoft.com/overview/serverless-computing/) environment without having to first create a VM or publish a web application. Individual functions run in the context of a function app, which is a Functions-specific code project in one of the [supported languages](https://docs.microsoft.com/azure/azure-functions/supported-languages), including [C#](#tab/csharp), [JavaScript](#tab/javascript), and [Java](#tab/java). When you use VSTS to build your function app project, you can automatically deploy your function app to Azure after every successful build.  

<!--note I am not going to even mention the built-in CI that's part of App Service :^) -->

## Create a function app in Azure

Before you can deploy your function app project from VSTS, you must first create a function app in Azure. The function app is the site in which your function app project runs. You can create a function app in Azure in one of the following ways:

* [Using the Azure CLI](https://docs.microsoft.com/azure/azure-functions/scripts/functions-cli-create-serverless).

* [From the Azure portal](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app).

* Publishing from [Visual Studio 2017](https://docs.microsoft.com/azure/azure-functions/functions-develop-vs#publish-to-azure) or [Visual Studio Code](https://code.visualstudio.com/tutorials/functions-extension/deploy-app).

## Prepare the project to run in Azure

Because the compressed file you deploy must be able to run in Azure, next you add tasks to obtain the required library files. If necessary, you also must also build the project.  

# [C#](#tab/csharp)

When you are deploying a function app developed by using C# in .NET class libraries (.csproj), you must restore NuGet packages in your project and build the project. You should add the following tasks to your pipeline:

* [Package: NuGet](../tasks/package/nuget.md)

* [Build: Visual Studio Build](../tasks/build/visual-studio-build.md)   

If your function app project uses C# script (.cxs) files, you do not need to add these tasks. 

# [JavaScript](#tab/javascript)

When you are deploying a JavaScript function app project, you should include the [Package: npm](../tasks/package/npm.md) task to restore the required packages. This action is not required for deployment, but it can significantly reduce start-up time the first time that your functions run.

# [Java](#tab/java)

When you are deploying a Java function app project, you should include the [Build: Maven](../tasks/build/maven.md) task to use Maven to build the app. 

<!-- Need to verify that this is actually true -->

## Generate a .zip file

The recommended way to deploy a function app project to Azure is from a .zip file. Because of this, you must include an **Archive files** task before your deployment task.  

## Configure the deployment task

When you deploy from a .zip file, all existing contents in the wwwroot folder are overwritten by the contents of the .zip file. When you use run-from-zip, the .zip file is mounted and files in the wwwroot folder are ignored.

### Choose the deployment method

### Add application settings

