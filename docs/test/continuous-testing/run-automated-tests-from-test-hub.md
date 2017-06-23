---
title: Run automated tests from test plans in the Test hub | Visual Studio Team Services and Team Foundation Server
description: Run automated tests on-demand against Team Foundation builds from test plans in the Test hub
ms.prod: vs-devops-alm
ms.technology: vs-devops-test-continuous
ms.assetid: 2886C58B-0F4B-4C0C-A248-3980CA629FD8 
ms.manager: douge
ms.author: ahomer
ms.date: 21/03/2017
---

# Run automated tests from test plans in the Test hub

**Team Services | TFS 2017 Update 2**

Automate test cases in your test plans and run them directly from the **Test** hub:

* Provides a user-friendly process for testers who may not be well
  versed with running tests in Build or Release workflows.

* Gives you the flexibility to run selected tests on demand,
  rather than scheduled testing in Build or Release workflows
  where all tests meeting the filter criteria are run.

* Useful when you want to rerun a few tests that failed due
  to test infrastructure issues, or you have a new build that
  includes fixes for failed tests.

<a name="prerequisites"></a>
You will need:

* A [test plan](../manual-exploratory-testing/getting-started/create-a-test-plan.md)
  containing your automated tests, which you have associated with automated test methods using 
  [Visual Studio 2017](associate-automated-test-with-test-case.md), 
  or [Visual Studio 2015 or earlier](https://msdn.microsoft.com/en-us/library/dd380741%28v=vs.120%29.aspx).

* A [Team Build definition](../../build/get-started/dot-net.md)
  that generates builds containing the test binaries.

* The app to test. You can deploy the app as part of the 
  [scheduled test workflow](example-continuous-testing.md) and also use it for on-demand testing.
  For information about setting up scheduled testing that also deploys the app, see
  [this blog post](https://blogs.msdn.microsoft.com/visualstudioalm/2017/03/26/vstest-task-dons-a-new-avatar-testing-with-unified-agents-and-phases/).

## Set up your environment

1. In the **Test plans** tab of the **Test** hub, choose your test plan,
   open the shortcut menu, and choose **Test plan settings**.

   ![Choosing Test plan settings](_img/run-automated-tests-from-test-hub/run-auto-tests-from-hub-101.png)

1. In the Test plan settings dialog, select the build definition that generates builds which
   contain the test binaries. You can then select a specific build number to test, or let the
   system automatically use the latest build when tests are run.

   ![Selecting the build and build number](_img/run-automated-tests-from-test-hub/run-auto-tests-from-hub-102.png)

1. You will need a release definition that was created from the 
   **Run automated tests from Test Manager** template to run tests from test plans
   in the **Test** hub. If you have an existing release definition that was created
   using this template, select it and then select the existing environment in the
   release definition where the tests will be executed.
   Otherwise, choose the **Create new** link in the
   dialog to create a new release definition containing a single environment
   with the **Visual Studio Test** task already added.

   ![Selecting a release definition or creating a new one](_img/run-automated-tests-from-test-hub/run-auto-tests-from-hub-102a.png)

1. To configure the **Visual Studio Test** task and the release definition,
   start by assigning meaningful names to the release definition and environment.
   Then select the **Visual Studio Test** task and configure it as follows:
 
   * Verify that version 2 of the Visual Studio Test task is selected.
     The version number is shown in the drop-down list at the top left
     of the task settings panel. 
 
   * Verify that **Select tests using** is set to **Test run (for on-demand-runs)**.
     [What does this setting mean?](#faq-ondemandruns) 

   * If you have UI tests that run on real browsers or thick clients,
     set (tick) the **Test mix contains UI tests** checkbox. This is not
     required if you are running UI tests on a headless browser. 

   * Select how is the test platform is provisioned, and the version of
     Visual Studio or the location of the test platform that is installed
     on the test machines 

   * If your tests need input parameters such as app URLs or database
     connection strings, select the relevant settings file from the
     build artifacts. You can use the **Publish build artifacts** tasks
     in you build definition to publish the settings file in a drop
     location if this file is not included in the artifacts.
     In the example shown below, the application URL is exposed in the
     run settings file, and is overridden to set it to a staging URL
     using the **Override test run parameters** setting.

   ![Specifying the properties for the Visual Studio Test task](_img/run-automated-tests-from-test-hub/run-auto-tests-from-hub-06.png)

1. Choose the **Run on agent** link and verify that the deployment queue
   is set to the one containing the machines where you want to run the
   tests. If your tests require special machines from the agent pool,
   you can add demands that will select these at runtime.

   ![Specifying the properties for the Agent phase](_img/run-automated-tests-from-test-hub/run-auto-tests-from-hub-04.png)

   You may be able to minimize test times by distributing tests across multiple
   agents by setting **Type of parallelism** to **Multi-agent** and specifying the number of agents.
   [More details](test-with-unified-agent-and-phases.md).

   > **Note**: If you are running UI tests such as CodeUI or Selenium
   on physical browsers such as IE, Firefox, or Chrome, the agent
   on the machines must be running in interactive mode and not
   as a service. [More details](#faq-agentmode). 

1. Open the **Artifacts** tab of the release definition and verify
   that the build definition containing the test binaries is linked
   to this release definition as an artifact source.  

   ![Verifying the linked build artifacts](_img/run-automated-tests-from-test-hub/run-auto-tests-from-hub-106.png)
 
1. Save the release definition.

1. If you chose **Create new** in the Test plan settings dialog in step 2
   of this example, return to the browser tab containing your test plan
   settings. In the Test plan settings dialog, select the release definition
   and environment you just saved.

   ![Selecting the release definition and environment](_img/run-automated-tests-from-test-hub/run-auto-tests-from-hub-107.png)

## Run the automated tests

1. In the **Test** hub, open the test plan and select a test suite that contains the
   automated tests.

1. Select the test(s) you want to run, open the **Run** menu,
   and choose **Run test**. 

   ![Selecting Run test](_img/run-automated-tests-from-test-hub/run-auto-tests-from-hub-108.png)

   The test binaries for these tests must be available
   in the build artifacts generated by your build definition.

1. Choose **OK** to start the testing process. The system checks that only
   automated tests are selected (any manual tests are ignored),
   validates the environment to ensure the Visual Studio Test
   task is present and has valid settings, checks the user's
   permission to create a release for the selected release
   definition, creates a test run, and then triggers the creation
   of a release to the selected environment.

   ![Starting the test execution](_img/run-automated-tests-from-test-hub/run-auto-tests-from-hub-109.png)

1. Choose **View test run** to view the test progress and analyze
   the failed tests. Test results have the relevant information
   for debugging failed tests such as the error message, stack trace,
   console logs, and attachments. 
 
1. After test execution is complete, the **Runs** tab of the
   **Test** hub shows the test results. The **Run summary** page
   shows an overview of the run.

   ![Viewing the test run summary](_img/run-automated-tests-from-test-hub/run-auto-tests-from-hub-110.png)
 
   There is a link to the **Release** used to run the tests, which
   makes it easy to find the release that ran the tests if you need
   to come back later and analyze the results. Also use this link if you
   want to open the release to view the release logs.

   [What are the typical error scenarios or issues I should look out for if my tests don't run?](#faq-errors)

1. The **Test results** page lists the results for each test in the
   test run. Select a test to see debugging information for failed
   tests such as the error message, stack trace, console logs, and attachments. 

   ![Viewing the test results details](_img/run-automated-tests-from-test-hub/run-auto-tests-from-hub-111.png)

1. Open the **Test Plans** page and select the test plan to see the status
   of your tests if tests are updated after test execution is complete.
   Select a test to see the recent test results.

   ![Viewing the test plan](_img/run-automated-tests-from-test-hub/run-auto-tests-from-hub-112.png)
 
## Q & A

<!-- BEGINSECTION class="m-qanda" -->

#### Q: Can I override the build or environment set at the test plan level for a specific instance of test run?

**A:** Yes, you can do this using the **Run with options** command.
Open the shortcut menu for the test suite in the left column and choose
**Run with options**.

![Configuring the Run with options dialog](_img/run-automated-tests-from-test-hub/run-auto-tests-from-hub-08.png)

Enter the following values in the Run with options dialog and then choose **OK**:

* **Test type and runner**: Select **Automated tests using Release environment**. 
  
* **Build**: Select the build that has the test binaries. The test results will be associated this build. 
 
* **Release Definition**: Select a definition from the list of release definitions that can consume the selected build artifact.
 
* **Release Environment**: Select the name of the environment configured in your release definition.<p />

![Configuring the Run with options dialog](_img/run-automated-tests-from-test-hub/run-auto-tests-from-hub-09a.png)

#### Q: Why use release environments to run tests? 

**A:** Release Management offers a compelling orchestration workflow
to obtain test binaries as artifacts and run tests. This workflow shares
the same concepts used in the scheduled testing workflow, meaning users
running tests in scheduled workflow will find it easy to adapt; for 
example, by cloning an existing scheduled testing release definition.

Another major benefit is the availability of a rich set of tasks in
the task catalog that enable a range of activates to be performed before
and after running tests. Examples include preparing and cleaning test data,
creating and cleaning configuration files, and more.

<a name="faq-ondemandruns"></a>
#### Q: How does selecting "Test run (for on-demand runs)" in the Visual Studio Test task work?

**A:** The Test management sub-system uses the test run object to
pass the list of tests selected for execution. The test task looks
up the test run identifier, extracts the test execution information
such as the container and test method names, runs the tests, updates
the test run results, and sets the test points associated with the
test results in the test run. From an auditing perspective, the 
Visual Studio task provides a trace from the historical releases
and the test run identifiers to the tests that were submitted for
on-demand test execution. 

<a name="faq-agentmode"></a>
#### Q: Should the agent run in interactive mode or as a service?

**A:** If you are running UI tests such as
[coded UI](https://docs.microsoft.com/en-us/visualstudio/test/use-ui-automation-to-test-your-code)
or [Selenium](getting-started/continuous-test-selenium.md) tests,
the agent on the test machines must be running in interactive mode,
not as a service, to allow the agent to launch a web browser. 
If you are using a headless browser such as [PhantomJS](http://phantomjs.org/),
the agent can be run as a service or in interactive mode. See 
[Build and Release Agents](../../build/concepts/agents/agents.md),
[Deploy an agent on Windows](../../build/actions/agents/v2-windows.md),
and [Agent pools and queues](../../build/concepts/agents/pools-queues.md). 

#### Q: Where can I find detailed documentation on how to run Selenium tests?

**A:** See [Get started with Selenium testing](getting-started/continuous-test-selenium.md). 

#### Q: What happens if I select multiple configurations for the same test?

**A:** Currently, the on-demand workflow is not configuration-aware. 
In future releases, we plan to pass configuration context to the test
method and report the appropriate results. 

#### Q: What if I need to download product binaries and test binaries from different builds? Or if I need to obtain artifacts from a source such as Jenkins?

**A:** The current capability is optimized for a single team build
to be tested on-demand using a Release Management workflow.
We will evaluate support for multi-artifact releases, including
non-Team Build artifacts such as Jenkins, based on user feedback. 

#### Q: I already have a scheduled testing release definition. Can I reuse the same definition to run test on-demand, or should I create a new definition as shown above? 

**A:** We recommend you use a separate release definition and environment for on-demand automated testing from the **Test** hub because:

* You may not want to deploy the app every time you want to run a few on-demand tests.
Scheduled testing environments are typically set up to deploy the product and then run tests. 

* New releases are triggered for every on-demand run. If you have many
testers executing a few on-demand test runs every day, your scheduled
testing release definition could be overloaded with releases for these
runs, making it difficult to find releases that were triggered for the
pipeline that contains scheduled testing and deployment to production. 

* You may want to configure the Visual Studio Test task with a Test run
identifier as an input so that you can trace what triggered the release.
See [How does selecting "Test run (for on-demand runs)" in the Visual Studio Test task work?](#faq-ondemandruns).

#### Q: Can I trigger these runs and view the results in Microsoft Test Manager?

**A:** No. MTM will not support running automated tests against Team Foundation
builds. It only works in the web-based interface for Team Services and TFS.
All new manual and automated testing product development investments will be
in the web-based interface. No further development is planned for MTM. See
[Guidance on Microsoft Test Manager usage](../manual-exploratory-testing/mtm/guidance-mtm-usage.md).

#### Q: I have multiple testers in my team. Can they run tests from different test suites or test plans in parallel using the same release definition?

**A:** They can use the same release definition to trigger multiple
test runs in parallel if:

* The agent pool associated with the environment has sufficient agents
to cater for parallel requests. If sufficient agents are not available,
runs can still be triggered but releases will be queued for processing
until agents are available.

* You have sufficient concurrent pipelines to enable concurrent releases.
See [Concurrent pipelines in Team Services](../../build/concepts/licensing/concurrent-pipelines-ts.md) 
or [Concurrent pipelines in TFS](../../build/concepts/licensing/concurrent-pipelines-tfs.md) for more information. 

* Testers do not run the same tests in parallel. Doing so may cause
results to be overwritten depending on the order of execution.

To enable multiple different test runs to execute in parallel, set the Release Management
environment trigger option for
[behavior when multiple releases are waiting to be deployed](../../build/concepts/definitions/release/triggers.md#env-triggers)
as follows:

* If your application supports tests running in parallel from different
sources, set this option to
**Allow multiple releases to be deployed at the same time**.

* If your application does not support tests running in parallel
from different sources, set this option to
**Allow only one active deployment at a time**. 

<a name="faq-errors".</a>
#### Q: What are the typical error scenarios or issues I should look out for if my tests don't run?

**A:** Check and resolve issues as follows:

* The release definition and environment in which I want to run tests
  are not shown after I select the build.
   - Make sure the build definition that is generating the build is linked
     as the primary artifact in the **Artifacts** tab of the release definition.<p />
 
* I get an error that I don't have sufficient permission to trigger a release.
   - Configure **Create releases** and **Manage deployments** permissions for
     the user in the **Security** menu of the release definition. 
     See [Release permissions](../../build/concepts/policies/permissions.md#release-permissions).<p />
   
* I get an error that no automated tests were found. 
   - Check the automation status of the selected tests. Do this in the work item
     for the test case, or use the **Column options** link in the **Test Plans**
     page of the **Test** hub to add the **Automation status** column to the list
     of tests. See the [pre-requisites section](#prerequisites) for information
     about automating manual tests.<p />

* My tests didn't execute, and I suspect the release definition is incorrect. 
   - Use the link in the **Run summary** page to access the release instance
     used to run the tests, and view the release logs.<p /> 

* My tests go into the error state, or remain "in-progress" even after release to the environment is triggered. 
   - Check if the release environment that you selected has the correct task
     and version selected. You must use version 2 or higher of the **Visual Studio
     Test** task. Version 1 of the task, and the **Run Functional Tests** task,
     are not supported.<p /> 

<!-- ENDSECTION -->

## See Also

* [Associate automated tests with test cases](associate-automated-test-with-test-case.md)
* [Associate automated test results with requirements](associate-automated-results-with-requirements.md)
* [Test with unified agents and phases](test-with-unified-agent-and-phases.md)
* [Continuous testing scenarios and capabilities](index.md)

[!INCLUDE [help-and-support-footer](../_shared/help-and-support-footer.md)] 
