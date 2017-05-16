---
title: Selenium testing in Visual Studio Team Services
description: UI Testing with Selenium in a continuous integration pipeline in Visual Studio Team Services (VSTS)
ms.prod: vs-devops-alm
ms.technology: vs-devops-test-continuous
ms.assetid: 1B90D2DF-4AB0-4B65-8039-2B14A25FB547
ms.topic: get-started-article
ms.manager: douge
ms.author: ahomer
ms.date: 08/12/2016
---

# Get started with Selenium testing in a continuous integration pipeline

[!INCLUDE [version-header-vs-tfs](../../_shared/version-header-vs-tfs.md)]

Performing user interface testing as part of the
build process is a great way of detecting
unexpected changes and need not be difficult. This
topic describes using Selenium to test your website
in a continuous integration build.

In this topic:

* [Create the test project](#create-project)
* [Include the test in a continuous integration build](#include-test)

For more information about Selenium browser automation, see:

* [Selenium HQ](http://docs.seleniumhq.org/)
* [Selenium documentation](http://www.seleniumhq.org/docs/01_introducing_selenium.jsp)

<a name="create-project"></a>
## Create the test project

As there is no template for Selenium testing, the
easiest way to get started is to use the Unit Test
template. This automatically adds the test framework
references and enables you run and view the results
from Visual Studio Test Explorer.

1. In Visual Studio, open the **File** menu and choose **New Project**,
   then choose **Test** and select **Unit Test Project**. Alternatively,
   open the shortcut menu for the solution and choose
   **Add** then **New Project** and then
   **Unit Test Project**. 

   For more details, see: [Get started with developer testing tools](../../developer-testing/getting-started/getting-started-with-developer-testing.md).

1. After the project is created, you must add the Selenium and
   browser driver references used by the browser to
   execute the tests. Open the shortcut menu for the
   Unit Test project and choose **Manage NuGet
   Packages**. Add the following packages to your project:

   * Selenium.WebDriver  (for Firefox)
   * Selenium.WebDriver.IEDriver
   * Selenium.WebDriver.ChromeDriver
   * Selenium.WebDriver.PhantomJS.Xplatform<p />

   ![Adding the browser driver packages to your solution](_img/continuous-test-selenium/continuous-test-selenium-02.png)

1. The Unit Test project creates a default class
   named **UnitTest1.cs**. To author a Selenium Test,
   replace the contents of the file with the following
   code.

         namespace Partsunlimited.UITests
         {
           using Microsoft.VisualStudio.TestTools.UnitTesting;
           using OpenQA.Selenium;
           using OpenQA.Selenium.Chrome;
           using OpenQA.Selenium.Firefox;
           using OpenQA.Selenium.IE;
           using OpenQA.Selenium.Remote;
           using OpenQA.Selenium.PhantomJS;
           using System;

           [TestClass]
           public class ChucksClass1
           {
             private string baseURL = "http://your-website.azurewebsites.net/";
             private RemoteWebDriver driver;
             private string browser;
             public TestContext TestContext { get; set; }

             [TestMethod]
             [TestCategory("Selenium")]
             [Priority(1)]
             [Owner("FireFox")]

             public void TireSearch_Any()
             {
               driver = new FirefoxDriver();
               driver.Manage().Window.Maximize();
               driver.Manage().Timeouts().ImplicitlyWait(TimeSpan.FromSeconds(30));
               driver.Navigate().GoToUrl(this.baseURL);
               driver.FindElementById("search - box").Clear();
               driver.FindElementById("search - box").SendKeys("tire");
               //do other Selenium things here!
             }

             [TestCleanup()]
             public void MyTestCleanup()
             {
               driver.Quit();
             }

             [TestInitialize()]
             public void MyTestInitialize()
             {
             }
           }
         }

   ![Replacing the code in UnitTest1.cs](_img/continuous-test-selenium/continuous-test-selenium-03.png)

1. Run the Selenium test locally using Test Explorer.

   ![Running the tests in Visual Studio Test Explorer](_img/continuous-test-selenium/continuous-test-selenium-04.png)

<a name="include-test"></a>
## Include the test in a continuous integration build

To include the Selenium test as part of a build,
the source code must be in version control.

![Checking the code into Visual Studio Team Services](_img/continuous-test-selenium/continuous-test-selenium-05.png)

### Create a continuous integration build definition

1. In your Visual Studio Team Services account where
   you checked in the test code, open the **Build &amp; Release** hub and select the **Builds** tab.

1. Create a new build definition using the **Visual Studio**
   build template. In the next page of the **Create new build definition**
   wizard:

   - Ensure that the repository and branch where you checked in your 
     code is selected.

   - Select the **Continuous integration...** checkbox so that
     your solution builds after each check-in using continuous integration.
 
   - Select the **Default** agent queue in which you have installed an agent.
     If you have not installed an agent in the **Default** queue, choose the
     **manage queues** link and do that now. For information about installing a build agent, see
     [Deploy a Windows build agent](../../../build/actions/agents/v2-windows.md).

   >Selenium tests will generally be run interactively, 
   which would fail on the **Hosted** build controller.
 
1. Choose **Create** to complete the **Create new build definition** wizard.

1. Delete the **Test Assemblies** (Visual Studio Test) task step from the build definition, then
   add a **Visual Studio Test Agent Deployment**, **Windows Machine File Copy**, and **Run Functional Tests**
   task from the **Test** and **Deploy** tabs of the task catalog. Drag and drop then in
   that order immediately after the **Publish symbols path** task step.

   ![Tasks in the build definition](_img/continuous-test-selenium/continuous-test-selenium-06.png)

1. Configure the tasks as shown in the following table.

   | Task step | Parameters |
   | --------- | ---------- |
   | ![Nuget Installer](../../../build/steps/package/_img/nuget-installer.png) [Package: Nuget Installer](../../../build/steps/package/nuget-installer.md)<br/>Install and update NuGet package dependencies. | **Path to solution or packages.config**: Select your app solution (.sln) file.<br/>**Installation type**: `Restore` |
   | ![Visual Studio Build](../../../build/steps/build/_img/visual-studio-build.png) [Build: Visual Studio Build](../../../build/steps/build/visual-studio-build.md)<br/>Build with MSBuild and set the Visual Studio version property. | **Solution**:  Select your app solution (.sln) file.<br/>**Platform**: `$(BuildPlatform)`<br/>**Configuration**: `$(BuildConfiguration)`<br/>**Visual Studio Version**: Select the version used to create your app. |
   | ![Index Sources &amp; Publish Symbols](../../../build/steps/build/_img/index-sources-publish-symbols.png) [Test: Index Sources &amp; Publish Symbols](../../../build/steps/build/index-sources-publish-symbols.md)<br/>Index the source code and optionally publish symbols to a SymStore file share. | **Search pattern**: `**\bin\**\*.pdb` |
   | ![Visual Studio Test Agent Deployment](../../../build/steps/test/_img/visual-studio-test-agent-deployment-icon.png) [Test: Visual Studio Test Agent Deployment](../../../build/steps/test/visual-studio-test-agent-deployment.md)<br/>Deploy and configure the test agent to run tests on a set of machines. | **Machines**: Comma-delimited list of machine names, or a variable containing the list.<br/>**Admin Login**: Username for target server or a variable containing it.<br/>**Admin Password**: Password for target server or a variable containing it.<br/>**Protocol**: `HTTP`<br/>**Select Machines By**: `Machine Names`<br/>**Agent Configuration - Username**: Agent username or a variable containing it.<br/>**Agent Configuration - Password**: Agent password or a variable containing it.<br/>**Agent Configuration - Interactive Process**: Checked |
   | ![Windows Machine File Copy](../../../build/steps/deploy/_img/windows-machine-file-copy-icon.png) [Deploy: Windows Machine File Copy](../../../build/steps/deploy/windows-machine-file-copy.md)<br/>Copy files to remote machines. | **Source**: `$(Build.Repository.LocalPath)`<br/>**Machines**: Comma-delimited list of machine names, or a variable containing the list.<br/>**Admin Login**: Username for target server or a variable containing it.<br/>**Password**: Password for target server or a variable containing it.<br/>**Destination Folder**: `C:\Deploy` or another folder on the target server. |
   | ![Run Functional Tests](../../../build/steps/test/_img/run-functional-tests-icon.png) [Test: Run Functional Tests](../../../build/steps/test/run-functional-tests.md)<br/>Run Coded UI tests, Selenium tests, and functional tests on a set of machines using the test agent. | **Machines**: Comma-delimited list of machine names, or a variable containing the list.<br/>**Test Drop Location**: `C:\Deploy` or the folder where you copied the files if different.<br/>**Execution Options - Test Selection**: `Test Assembly`<br/>**Execution Options - Test Assembly**: `**\*Test*.dll` |
   | ![Copy Files](../../../build/steps/utility/_img/copy-files.png) [Test: Copy Files](../../../build/steps/utility/copy-files.md)<br/>Copy files from a source folder to a target folder using match patterns. | **Source Folder**: `$(build.sourcesdirectory)`<br/>**Contents**: `**\bin\$(BuildConfiguration)\**`<br/>**Target Folder**: `$(build.artifactstagingdirectory)` |
   | ![Publish Build Artifacts](../../../build/steps/utility/_img/publish-build-artifacts.png) [Test: Publish Build Artifacts](../../../build/steps/utility/publish-build-artifacts.md)<br/>Publish Build artifacts to the server or a file share. | **Path to Publish**: Select your Azure subscription.<br/>**Artifact Name**: `drop`<br/>**Artifact Type**: `Server` |

   >It's generally advisable to use custom variables for parameter values, especially
   where the same value is used in the parameters of more than one task. You can also 
   secure and hide values by using custom variables. See [Build Variables](../../../build/define/variables.md). 

1. Save the build definition and queue a new build.

1. To validate the test results from a build, open
   the build summary from the **Explorer** tab.

   ![Selecting a build result](_img/continuous-test-selenium/continuous-test-selenium-09.png)

   The build summary includes a snapshot of the test
   results. There is also a **Tests** results page that
   highlights the build-on-build changes, including
   errors, stack traces, and the ability to easily
   create a bug that contains this information.

   ![The build summary and test results](_img/continuous-test-selenium/continuous-test-selenium-10.png)

## Also see

* [Use Selenium with cloud-based load testing](http://blogs.msdn.com/visualstudioalm/archive/2014/11/17/using-selenium-with-cloud-load-testing.aspx)
* [Run tests with builds](getting-started-with-continuous-testing.md)
* [Create your Visual Studio Team Services Account](http://visualstudio.com/)
* [Get started with developer testing tools](../../developer-testing/getting-started/getting-started-with-developer-testing.md)

For more information about Selenium browser automation, see:

* [Selenium HQ](http://docs.seleniumhq.org/)
* [Selenium documentation](http://www.seleniumhq.org/docs/01_introducing_selenium.jsp)

For information about deploying PhantomJS.exe as part of your test, see [this blog post](http://blogs.msdn.com/visualstudioalm/archive/2014/11/17/using-selenium-with-cloud-load-testing.aspx).

[!INCLUDE [help-and-support-footer](../../_shared/help-and-support-footer.md)]
