---
title: Continuous integration, test, and deployment example with Visual Studio Team Services and Team Foundation Server
description: Continuous integration, test, and deployment example using Visual Studio Team Services (VSTS) or Team Foundation Server (TFS)
ms.prod: vs-devops-alm
ms.technology: vs-devops-test-continuous
ms.assetid: 447F1F56-993A-4AB0-B521-ED72514BDEE3
ms.manager: douge
ms.author: ahomer
ms.date: 08/12/2016
---

# Continuous integration, test, and deployment example

**Visual Studio 2017 | Visual Studio  2015 | Team Services** 

This walk-through demonstrates how you can use the continuous integration and
continuous deployment features of Visual Studio Team Services and
Microsoft Team Foundation Server (TFS) to build, test, and deploy
applications quickly and efficiently to Azure App Services; and
run a simple performance test after deploying every update.

The walk-through is divided into the following sections:

* [Create the Azure app service instance for your sample app](#create-service).
* [Create and check in a sample ASP.NET MVC web app containing unit tests](#create-app).
* [Configure continuous integration (CI) to build the sample application and run the unit tests](#configure-ci).
* [Configure continuous deployment (CD) to deploy the sample app and run a quick performance test](#configure-cd).
* [Modify the sample app to explore behavior when a test fails](#test-failure).
* [Fix the test failure and view the complete CI/CD process](#view-process).

It will take around 45 minutes to complete all of the steps.

<a name="create-service"></a>
## Create the Azure app service 

In this section, you'll create the Azure app service instance you'll need to deploy the app. 

1. Sign into the [Azure portal](https://portal.azure.com) using the same credentials as your Visual Studio Team Services
   account, choose **App Services**, and add a new service instance. 
 
   ![Creating an Azure app service instance, adding a new service](_img/example-continuous-testing/example-continuous-testing-01.png)

1. Select the simple **Web App** type for your new service.

   ![Creating an Azure app service instance, choosing the type](_img/example-continuous-testing/example-continuous-testing-02.png)

1. In the confirmation page, choose **Create**.

   ![Creating an Azure app service instance, starting to create](_img/example-continuous-testing/example-continuous-testing-03.png)
1. Enter a name for the new Web App instance and the new Resource Group, then
   choose **Create**. 
 
   ![Creating an Azure app service instance, entering the parameters](_img/example-continuous-testing/example-continuous-testing-04.png)

1. In the navigation bar, select **All resources** and check that the list
   contains the new App Service instance. It may take a few minutes to be fully available.

   ![Creating an Azure app service instance, checking for the new instance](_img/example-continuous-testing/example-continuous-testing-05.png)

>For more details about creating web apps in Azure App Services, see
[Azure Web Apps Documentation](https://docs.microsoft.com/azure/app-service-web/)

<a name="create-app"></a>
## Create the sample web app

In this section, you will create a simple ASP.NET MVC web app containing 
unit tests that you can execute as part of the build process. 

1. In Visual Studio, create a new **ASP.NET Web Application** project from
   the **Web** section of the list of installed templates.

   ![Creating the new project](_img/example-continuous-testing/example-continuous-testing-10.png)

1. When prompted, select **MVC** template and make sure to set (tick) the **Add unit tests** checkbox. 

   ![Including unit tests in your project](_img/example-continuous-testing/example-continuous-testing-11.png)

1. Save and close the new project, then check it into your Visual Studio Team Services or
   Team Foundation Server repository. 

   ![Checking the sample app into the repository](_img/example-continuous-testing/example-continuous-testing-12.png)

>For more details about creating apps in Visual Studio, see
[Solutions and Projects in Visual Studio](https://docs.microsoft.com/visualstudio/ide/solutions-and-projects-in-visual-studio).
For more details about using Team Services code repositories, see
[Share your code with Visual Studio and Team Services Git](../../git/share-your-code-in-git-vs.md).

<a name="configure-ci"></a>
## Configure continuous integration

In this section, you will create a build definition that is configured to
run automatically when you check in any changes to the sample app, and it
will automatically execute the unit tests it contains.

1. Sign into your Visual Studio Team Services account (**https://**_your-acccount_**.visualstudio.com**)
   and open the project where you checked in the sample app.

1. Open the **Build &amp; Release** hub and, in the **Builds** tab, choose
   **+ New definition**. 

   ![Starting a new build definition](_img/example-continuous-testing/example-continuous-testing-20.png)

1. Choose the **ASP.NET** template for the new build definition.

   ![Choosing the build type](_img/example-continuous-testing/example-continuous-testing-21.png)

1. In the next page of the wizard, make sure you set (tick) the **Continuous integration...** checkbox, 
   then choose **Create**.

   ![Specifying continuous integration](_img/example-continuous-testing/example-continuous-testing-22.png)

1. For the **NuGet restore** task in the new definition, use the file selector to select the
   solution file for your sample web app.

   ![Specifying the source solution for the Nuget task](_img/example-continuous-testing/example-continuous-testing-25.png)

1. For the **Build solution** task, use the file selector to select the
   solution file for your sample web app and choose the version of
   Visual Studio you used to create the app. 

   ![Specifying the source solution for the Visual Studio Build task](_img/example-continuous-testing/example-continuous-testing-26.png)

1. Save the new build definition.

   ![Saving the definition](_img/example-continuous-testing/example-continuous-testing-27.png)

1. Queue a new build of the definition.

   ![Starting a test build](_img/example-continuous-testing/example-continuous-testing-28.png)

1. After the build has finished, you see the summary for each task and the results in the live log file.
   Choose the **Tests** link.

   ![Viewing the build results](_img/example-continuous-testing/example-continuous-testing-29.png)

1. The **Tests** tab provides comprehensive results of executing the unit tests defined in the
   solution. Use the **Outcome** list to show the tests that passed.

   ![Viewing the test results](_img/example-continuous-testing/example-continuous-testing-30.png)

   [What are the typical types of tests I can use to validate my app?](#qa-more-tests)

1. Choose the test summary item at the top of the list of tests to open the **Test** hub
   in a new browser window, showing a summary and charts for this test run.

   ![Viewing the test results](_img/example-continuous-testing/example-continuous-testing-31.png)

>For more details about build definitions in Team Services, see
[Continuous integration on any platform](../../build/overview.md). For more details about unit tests and the results, see 
[Get started with developer testing tools](../developer-testing/getting-started/getting-started-with-developer-testing.md).

<a name="configure-cd"></a>
## Configure continuous deployment

In this section, you will create a release definition that is configured to
start a release that deploys the app automatically when a successful build
occurs. After successful deployment, the release will automatically execute
a simple performance test to validate the deployment.

1. Close the **Test** hub browser window and, in the build summary page in
   the **Builds** hub, choose the **Release** icon and then choose **OK** to
   confirm.

   ![Starting a new release definition ](_img/example-continuous-testing/example-continuous-testing-40.png)

1. Select the **Azure App Service Deployment with Performance Test** template.

   ![Selecting the release definition template](_img/example-continuous-testing/example-continuous-testing-41.png)

1. In the next page of the wizard, check that the correct **Source (Build definition)**
   is selected and make sure your set (tick) the **Continuous deployment** checkbox. 
   Then choose **Create**.
 
   ![Specifying continuous deployment ](_img/example-continuous-testing/example-continuous-testing-42.png)

1. In the new release definition, choose the "pencil" edit icon next to the default
   name and enter some meaningful name. Press _RETURN_ to save it.

   ![Editing the definition name](_img/example-continuous-testing/example-continuous-testing-43.png)

1. In the new release definition, select the **Deploy Azure App Service** task.
   In the parameters pane, select your Azure subscription from the drop-down list and
   choose **Authorize** to validate it. Then select your App Service name 
   from the drop-down list. 

   ![Configuring the Deploy Azure App Service task](_img/example-continuous-testing/example-continuous-testing-44.png)

   If you don't see any subscriptions listed, choose the **Manage** link and, in the 
   **Services** page, create a new **Azure Resource Manager** service endpoint. If you
   have problems creating the connection, see 
   [Troubleshoot Azure Resource Manager service endpoints](../../build/actions/azure-rm-endpoint.md).

   ![Creating an Azure service connection ](_img/example-continuous-testing/example-continuous-testing-44a.png)

   [Can I deploy to a staging slot first, and then to production?](#qa-stagingslot)

1. Select the **Quick Web Performance Test** task and, in the parameters pane,
   enter the full URL of your Azure App Service instance. 

   ![Configuring the Quick Web Performance Test task](_img/example-continuous-testing/example-continuous-testing-46.png)

   You can get the full URL from the **Overview** page for your App Service instance
   in the Azure portal. The URL will be in the form **http://**_your-app-service-name_.**azurewebsites.net**.

   ![Finding the app service instance URL](_img/example-continuous-testing/example-continuous-testing-45.png)

   [What other tests can I run to validate my deployment?](#qa-more-tests)

1. Save the new release definition.

   ![Saving the release definition](_img/example-continuous-testing/example-continuous-testing-47.png)

1. Create a release from your definition using the **Release** icon in the toolbar.

   ![Creating a new release](_img/example-continuous-testing/example-continuous-testing-48.png)

1. After the release starts, choose the **Release-**_x_ link just below the toolbar.

   ![Selecting the link to the new release](_img/example-continuous-testing/example-continuous-testing-49.png)

1. This shows a summary of the release, with the Deployment status as **IN PROGRESS**. Choose
   the **Logs** link above the toolbar.

   ![Selecting the Logs link in the release summary page](_img/example-continuous-testing/example-continuous-testing-50.png)

1. The **Logs** page shows the status of each step in the release, and a live log. 
   When  the release has successfully completed, choose the **Summary** link above the toolbar.

   ![Selecting the Summary link in the logs page](_img/example-continuous-testing/example-continuous-testing-51.png)

1. The **Summary** page shows the final release summary, and the load test results
   ("No thresholds violated").

   ![Viewing the final release summary](_img/example-continuous-testing/example-continuous-testing-52.png)

1. Open the **Load test** tab of the **Test** hub. This shows a summary of all 
   the load test runs you have executed. Open the **LoadTest.loadtest** run that
   was just completed, 

   ![Viewing all the load test runs](_img/example-continuous-testing/example-continuous-testing-53.png)

1. As well as the **Summary** page for the load test run, you can open the
   **Charts**, **Diagnostics**, and **Logs** tabs to see more information about the test run.

   ![Viewing details of the load test run](_img/example-continuous-testing/example-continuous-testing-54.png)

   >For more details about release definitions, see
   [Release Management in Team Services](../../build/concepts/definitions/release/index.md). For more details about load tests and the results, see 
   [Run URL-based load tests with Visual Studio Team Services](../performance-testing/getting-started/get-started-simple-cloud-load-test.md).

<a name="test-failure"></a>
## Explore behavior when a test fails

In this section, you will modify the sample app so that one of the unit tests
will fail, and see how the CI/CD process is halted when the test fails during
the build process.

1. In Visual Studio, open the source solution for your app and open the
   **HomeController.cs** file from the **Controllers** folder of your main 
   app project (in this example, it's SampleWebAppWithTests\Controllers\HomeController.cs).

1. Change the line in the **About** method to show a different message, such as: 

   ```
   public ActionResult About()
   {
     ViewBag.Message = "My super new web app.";
     return View();
   }
   ```

1. Save the change and check in the change to your Team Services repository.

1. Open the **Builds** tab of the **Build &amp; Release** hub. You'll see
   a build of your build definition in "_in progress_". Choose the build number link 
   next to this to open the build summary.

   ![Viewing the CI build in progress](_img/example-continuous-testing/example-continuous-testing-60.png)

1. In the build summary, you can see the message that one of the unit tests failed,
   and that there was no deployment from this build. Because the test failed, Team 
   Services did not automatically create a CD release.

   ![Viewing the result of the failed CI build](_img/example-continuous-testing/example-continuous-testing-61.png)

1. Choose the **Test** link to open the test details tab. You can see a summary
   of the test run, and - by default - a list of the failed tests. Choose the one
   failed test to see details. The error message shows that the description for the
   **About** method (which you edited) does not match the expected value.

   ![Viewing the detailed test results](_img/example-continuous-testing/example-continuous-testing-62.png)

1. Verify that the new build did not start a CD release by opening the
   **Releases** tab of the **Build &amp; Release** hub. You can see that there is
   only the first release you created manually earlier in this example.

   ![Checking if any release is in progress](_img/example-continuous-testing/example-continuous-testing-63.png)

<a name="view-process"></a>
## View the complete CI/CD process

In this section, you will fix the failing test, check in the updates, and
see the complete CI/CD process execute; finishing with the results of the
post-deployment performance test.

1. Go back to your source solution in Visual Studio and open the
   **HomeControllerTest.cs** file from the **Controllers** folder of the
   **Tests** project (in this example, it's SampleWebAppWithTests.Tests\Controllers\HomeControllerTest.cs).

1. Change the line in the **About** test method so that it matches the
   message you specified when you edited the main project earlier. In this example: 

   ```
   [TestMethod]
   public void About()
   {
     // Arrange
     HomeController controller = new HomeController();

     // Act
     ViewResult result = controller.About() as ViewResult;

     // Assert
     Assert.AreEqual("My super new web app.", result.ViewBag.Message);
   }

   ```

1. Save the change and check in the change to your Team Services repository.

1. Open the **Builds** tab of the **Build &amp; Release** hub. You'll see
   a build of your build definition in "_in progress_". Choose the build number link 
   next to this to open the build summary and check that it succeeds.

1. Choose the **Test** link to open the test details tab. You'll see
   that all the tests passed.

1. Verify that the new build did start a CD release by opening the
   **Releases** tab of the **Build &amp; Release** hub. This time you
   see a new release in progress.

   ![Checking that a release is in progress](_img/example-continuous-testing/example-continuous-testing-70.png)

1. In your web browser, open your new ASP.NET website. The URL will be in 
vthe form **http://**_your-app-service-name_.**azurewebsites.net**.

   ![Viewing the final result website](_img/example-continuous-testing/example-continuous-testing-71.png)

## Q & A

<a name="qa-stagingslot"></a>
### Q: Can I deploy to a staging slot first, and then to production?

**A**: Yes, you can create additional deployment slots in Azure Web Apps,
and specify which slot to deploy your app to. If you do not specify a slot,
the default **Production** slot is used. After you deploy, you can swap an
app to a different slot using the **Azure App Service Manage** task. See
[Swap deployment slots](../../build/apps/cd/deploy-webdeploy-webapps.md#swap-deployment-slots).

You can use [task phases](../../build/concepts/process/phases.md)
and the [**Manual Intervention**](../../build/concepts/process/phases.md#the-manual-intervention-task) task
in your release definition to pause a deployment; for example, to examine test results
after the load tests have run and before the app is swapped from staging to production. 

<a name="qa-more-tests"></a>
### Q: What are the typical types of tests I can run to validate my app and deployment?

**A**: Testing in a continuous integration and continuous deployment (CI/CD) scenario typically consists of:

1. Run **unit tests** in the CI pipeline, as demonstrated in the example above. The **Visual Studio Test** task
   automatically runs tests included in the app assemblies, but there is a wide range of configuration options
   you can specify, such as running only specific tests. See [Run Tests using Visual Studio task](https://github.com/Microsoft/vsts-tasks/blob/releases/m109/Tasks/VsTest/README.md).
 
1. Run **functional tests** in the early stages of the CD pipeline. These are typically 
   [Selenium](getting-started/continuous-test-selenium.md) (for web apps) and [Coded UI](https://msdn.microsoft.com/en-us/library/dd286726.aspx) tests.
   To do this, add the **[Deploy Test Agent](https://github.com/Microsoft/vsts-tasks/blob/releases/m109/Tasks/DeployVisualStudioTestAgent/README.md)**
   and **[Run Functional Tests](https://github.com/Microsoft/vsts-tasks/blob/master/Tasks/RunDistributedTests/README.md)**
   tasks to your release definition. See [Testing in Continuous Integration and Continuous Deployment Workflows](https://blogs.msdn.microsoft.com/visualstudioalm/2015/05/29/testing-in-continuous-integration-and-continuous-deployment-workflows/).

1. Run **load tests** after the app is deployed to staging and production, after it passes all functional tests.
   The example shown above is just a simple test that accesses a single page in the web app to validate that 
   deployment succeeded and the app is running successfully. You can perform must more comprehensive load testing
   to validate the entire app by running [cloud-based load tests](../../build/steps/test/cloud-based-load-test.md)
   and [Apache JMeter load tests](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/RunJMeterLoadTest).

## Related topics

* [Continuous integration on any platform](../../build/overview.md)
* [Get started with continuous testing](getting-started/getting-started-with-continuous-testing.md)
* [Git and Team Services](../../git/overview.md)
* [More examples](../../build/apps/index.md)

[!INCLUDE [help-and-support-footer](../_shared/help-and-support-footer.md)] 
