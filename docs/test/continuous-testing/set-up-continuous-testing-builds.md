---
title: Set up continuous testing for your builds - Visual Studio Team Services and Team Foundation Server
description: Set up continuous testing for your builds in Visual Studio Team Services (VSTS) or Team Foundation Server (TFS)
ms.prod: vs-devops-alm
ms.technology: vs-devops-test-continuous
ms.assetid: 7849EF41-BE1A-4342-B1DA-583DB6DD1831
ms.manager: douge
ms.author: ahomer
ms.date: 06/15/2017
---

# Set up continuous testing for your builds

[!INCLUDE [version-header-ts-tfs](../_shared/version-header-ts-tfs.md)]

Find problems early after changes are checked in and built by running continuous tests using Visual Studio Team Services or Team Foundation Server.

Before you start:

* [Create a build definition](../../build/overview.md) that builds your solution after each check-in, using continuous integration.

* [Set up environments](set-up-continuous-test-environments-builds.md) to run your app and tests remotely in a distributed environment after each build.

## Step 1: Set up app deployment for your build

1. In Visual Studio Team Services or Team Foundation Server, go to your team project.

1. Go to your build definition. Add steps to deploy your app for testing. For example, if you're testing a Visual Studio solution:

   ![Edit build definition](../_img/edit-build-definition.png)

   ![Add a step to your build definition](_img/set-up-continuous-testing-builds/add-build-step.png)

   ![Add File Copy and PowerShell steps](_img/set-up-continuous-testing-builds/add-file-copy-powershell-steps.png)

1. Add the details to copy your app from its drop location to its test environment:

   * Source folder for your app

   * List of machines where you want to deploy your app

   * Credentials to connect to the target machines  

   * Target folder where to put your app

   ![Build definition, copy app details](_img/set-up-continuous-testing-builds/copy-app-test-environment.png)

   > If you use the list of machines in more than one task, consider defining
   a variable that contains the list of machines. For example, a
   [build or release definition variable](../../build/concepts/definitions/release/variables.md)
   or a variable defined within a project-wide 
   [variable group](../../build/concepts/library/variable-groups.md).
   Using a variable means that you can change the list of machines in one place
   and have the change apply to all the tasks that use the variable.

1. Add the details to deploy your app using PowerShell:

   * List of machines where you want to deploy your app

   * Credentials to connect to the target machines  

   * Path to the PowerShell script used to deploy your app

   ![Add step to deploy app with PowerShell](_img/set-up-continuous-testing-builds/run-powershell-details.png)

1. Save your build definition.

   ![Build definition: save](_img/set-up-continuous-testing-builds/save-build-definition.png)

## Step 2: Set up test deployment for your build

1. In your build definition, add a step with these details to deploy your tests:

   * Source folder for your tests

   * List of machines where you want to run your tests

   * Credentials to connect to the target machines  

   * Target folder where to put your tests

   ![Build definition, copy tests](_img/set-up-continuous-testing-builds/copy-tests.png)

1. Add a step with these details to deploy the test agent for running your tests:

   * List of machines where you want to deploy the test agent

   * Credentials to connect to the target machines  

   * Credentials for the deployment agents, so the test agent can run in your test environment

   ![Build definition: deploy test agent details](_img/set-up-continuous-testing-builds/deploy-test-agent.png)

1. Save your build definition.

   ![Build definition: save](_img/set-up-continuous-testing-builds/save-build-definition.png)

## Step 3: Set up your tests to run with your build

1. In your build definition, add a step with these details to run your tests with the test agent:

   * List of machines where you want to run your tests

   * Folder where you put your tests

   ![Build definition: Run tests with test agent](_img/set-up-continuous-testing-builds/run-tests-with-test-agent.png)

1. Save your build definition.

   ![Build definition: save](_img/set-up-continuous-testing-builds/save-build-definition.png)

1. To check your test run, queue your build.

   ![Build definition: queue build](../_img/queue-build.png)

1. After your build is done, [review your test results](getting-started/review-continuous-test-results-after-build.md).

## Q & A

<!-- BEGINSECTION class="m-qanda" -->

#### Q: What if I want to run debug builds of native (.cpp) unit tests on the machine with the test agent?

**A**: Make sure that you have debug versions of the Universal C Runtime (UCRT) on the machine with the test agent, specifically these libraries: ucrtbased.dll and vcruntime140d.dll. You can include these items with your deployment.

If you're running release builds of .cpp unit tests, make sure that you have Windows Update KB2999226 on your test agent machine.

#### Q: I'm having problems using xUnit with .NET Core apps. Where can I get more information?

**A**: See the blog post [Unit Tests with .NET Core and Visual Studio Team Services](http://blogs.perficient.com/microsoft/2016/08/unit-test-with-net-core-and-vsts/).

<!-- ENDSECTION -->

## See also

* [Set up environments for continuous testing with your builds](set-up-continuous-test-environments-builds.md)
* [Review continuous test results after a build](getting-started/review-continuous-test-results-after-build.md)
* [Run tests with your builds](getting-started/getting-started-with-continuous-testing.md)
* [End-to-end example of continuous testing](example-continuous-testing.md)

[!INCLUDE [help-and-support-footer](../_shared/help-and-support-footer.md)] 
