<!-- Q & A for performance-testing topics -->

## Q&A

* General
* [Set up tests](#set-up-tests)
* [Apache JMeter tests](#jmeter-tests)
* [Run and monitor tests](#run-monitor-tests)
* [Troubleshooting](#troubleshooting)
* [Errors](#errors)

<!-- BEGINSECTION class="md-qanda" -->

### General

#### Q: How do I learn more about Cloud-based Load Testing?

A: Watch this video, or check out the 
[Cloud-based Load Testing blog](http://aka.ms/loadtestkb). 

<iframe src="//channel9.msdn.com/Events/Visual-Studio/Launch-2013/QE103/player" width="600" height="315" allowFullScreen="true" frameBorder="0"></iframe>

#### Q: Do I need anything to load test in the cloud with Visual Studio Ultimate 2013?

A:  Yes, you'll need Update 4 or Update 5 installed. [Download this version](https://www.visualstudio.com/downloads/download-visual-studio-vs).

#### Q: My Visual Studio trial period ended, but I still want to run load tests.

A:  To continue load testing after the trial, you'll need an active and valid 
Visual Studio Enterprise 2017 or 2015 license, or a Visual Studio Ultimate 2013 license. 
[Learn more about licensing](https://www.visualstudio.com/products/how-to-buy-vs).

#### Q: Can I run cloud-based load tests on any app, even behind a firewall?

A:  Yes, you can load test apps or sites that are only available to your company, 
like internal or pre-release apps, staging or preproduction deployments. To learn more, see 
[Testing private and intranet applications using cloud-based load testing](https://blogs.msdn.microsoft.com/visualstudioalm/2016/08/23/testing-privateintranet-applications-using-cloud-based-load-testing/).

Or, you can 
[run a load test locally using Visual Studio](../performance-testing/run-performance-tests-app-before-release.md).

#### Q: What are virtual users?

A:  Virtual users create load by accessing your app or web site all at the same 
time during your test run. That way, you can test performance under more realistic 
or projected conditions. Virtual users are simulated by test agents.

#### Q: What are test agents? How do they relate to my test run?

A: Test agents are computing resources, like CPU, memory, and network, 
that generate load by simulating virtual users. Test agents use agent cores 
to create virtual users. Each core creates at least 1 virtual user. 

For load test runs in Visual Studio Team Services with the Visual Studio IDE,
you can specify the number of cores to use. For example,
if you get errors when you run your test, 
you might have to increase the number of cores.

Otherwise, your tests and the number of virtual users that 
you specify determine how many cores and agents are used.

#### Q: Where do I specify the number of cores for runs in Visual Studio Team Services with the Visual Studio IDE?

A: You can do that here:

![Update the agent count total cores](../_img/LoadTestAgentsCores.png)

What do the values mean?

| Cores | Agents |
| --- | --- | 
| 0 | (Default) The number of cores is based on the number of virtual users that you specify for your test. |
| 1 | Your test run will use 1 agent. |
| 2 - 10 | Each agent will always use 2 cores. |
| 11 - 40 | Each agent will always use 4 cores. |
| 41 - 200 | Each agent will always use 8 cores. |

The maximum number of cores for each test run is 200. 
If your test run needs more cores, you can run up to 10 load tests at the same time.

The minimum number of virtual users per agent core is 1. 
If your load test requires more cores, contact
[vsoloadtest@microsoft.com](mailto:vsoloadtest@microsoft.com).

The number of agents also depends on your text mix (web performance test or unit test). 
If you have only web performance tests, we suggest using between 600 and 2,500 virtual users for every two cores. 
If you have unit tests, the agent count depends on what your unit tests do. 
This means you will have to test if you have enough agents by 
running a shorter duration load test run or use 
[goal-based load testing](http://blogs.msdn.com/b/visualstudioalm/archive/2015/08/03/announcing-support-for-goal-based-load-pattern-in-cloud-based-load-tests.aspx).

<a name="VUM"></a>
#### Q: What are virtual user minutes (VUMs)? How many minutes will my load test use?

A: If your test run uses 25 or more virtual users per core, 
then VUMs = (max virtual user load for your test run) * (test run duration in minutes).

If your test run uses fewer than 25 users per core, then VUMs = 
(number of cores) \* (25 virtual users per core) \* (test run duration in minutes).

The minimum values used to calculate VUMs are 25 virtual users and 1 minute. 
If your test run values are smaller than the minimum values, 
then those values are rounded up to meet the minimums. 
For example, if your test run specifies 20 virtual users for 30 seconds,
then your test run will actually run with 25 virtual users for 1 minute = 25 VUMs, 
not 15 VUMs.
 
Also, test run duration is in minutes, not seconds. For example, 
if your test run duration is 5 minutes and 15 seconds, 
then that duration is rounded up to 6 minutes. 
   
A minimum of 250 virtual user minutes, including the warm-up period, is deducted from your account for:

* Completed runs, based on the full duration of the run
* Aborted runs, based on the elapsed run duration

For runs that end in an error state, no virtual user minutes will be deducted from your account.

Note that there is an additional charge for [resource retention](#retain-resources).

To check how many virtual user minutes that your Visual Studio Team Services account 
has used or has remaining, go to your Visual Studio Team Services account home page 
(```https://{youraccount}.visualstudio.com```).

<a name="test-limits"></a>
#### Q: Are there any limits when running the cloud-based load tests?

A: Yes. Based on where you're running the test, each test run duration limit is:

* Visual Studio IDE: 48 hours
* Visual Studio Team Services Load test hub:
 - URL-based load tests: 48 hours
 - JMeter load tests: 4 hours
* Azure portal: 1 hour

#### Q: Do other load tests run on the same virtual machines that host my agents?

A:  No, the virtual machines that host your agents host only one load test run.

#### Q: Are there load test features that aren't supported when you run load tests in the cloud?

A: These features aren't currently supported:

*   Network mix property
*   Agent to Use in test settings - use the core count property instead
*   SQL Trace properties in run settings
*   IP switching

<a name="retain-resources"></a>
#### Q: Can I speed up my load testing cycle by retaining the resources the tests use?

A: Yes, you can reduce the delay while your load test starts each time during a typical 
test &gt; fix &gt; retest scenario by retaining the resources for an appropriate period 
after each test completes, instead of having to wait for them to be acquired and 
provisioned for each test run. In Visual Studio Update 3
and later, specify the retention time in your run settings properties.

![Specify resource retention time in Visual Studio 2017 and Visual Studio 2015 Update 3 and higher](../_img/resource-retain-time01.png)

In earlier versions of Visual Studio, add a context parameter named **ResourcesRetentionTimeInMinutes**
to your run settings.

![Specify resource retention time in Visual Studio 2015 pre Update 3](../_img/resource-retain-time02.png)

Note:

* The maximum resource retention period is 4 hours (240 minutes).

* The resources will be released after the specified period if you do not start another 
test during that period. When you start another test, the resource retention period you 
specify in that test will be applied - effectively allowing you to extend the retention 
period. You can specify a different retention period each time you start a test.

* There a small additional charge applied when you use this feature. In addition to 
the usual VUMs that your load test consumes, a surcharge of 5 VUMs per core is applied
for the duration of the run. So if you retain 20 cores for 10 minutes, an additional
1000 VUMs (5 x 20 x 10) will be charged. The status messages display this information.

* Resource retention is not available for Apache JMeter tests at the present time.

For more details, see [this blog post](https://blogs.msdn.microsoft.com/visualstudioalm/2016/07/18/speed-up-cloud-load-test-execution-by-retaining-resources-for-quick-consecutive-runs/).

<a name="set-up-tests"></a>
### Set up tests

#### Q: Can I have other test types, besides web performance tests, in a load test mix?

A: Yes, you can include unit tests and coded web tests, but not coded UI tests.

#### Q: How long do I have to wait until I can run my load test after creating a Visual Studio Team Services account?

A:  It can take between 5 seconds to 3 hours until you get permissions 
to run the load test in the cloud. If you previously created your Visual Studio Team Services account, 
you might be able to run the load test right away.

#### Q: How do I provide different values to the same test?

A:  Use a .csv file or an Excel spreadsheet. Using SQL Server is currently not supported. 
Learn how to [supply values to your test](https://msdn.microsoft.com/library/ms243142.aspx).

#### Q: Help, I'm having problems with my agents!

A: You must have at least 1 virtual user per core. If you're getting status 
messages that an agent stopped working due to load, 
or if the downloaded report shows high CPU use for an agent, 
try increasing the number of agents that you're using. 

If you need more help, contact 
[vsoloadtest@microsoft.com](mailto:vsoloadtest@microsoft.com)

#### Q: Where are the test agents used for my load test runs located?

A:  When you set up your load test run, you can select the test agent location from any supported Azure datacenter, starting with Visual Studio Ultimate 2013 Update 5 and Visual Studio Enterprise 2015. 
After your run finishes, your results are stored in the same location as your Visual Studio Team Services account.

![Edit load test to set location](../_img/CLT_LoadTestSetLocation.png)

If you're using an earlier version of Visual Studio, 
the agent location is based on the location that you chose 
when you created your Visual Studio Team Services account.

| Visual Studio Team Services Account Region | Test Agent Azure Datacenter |
| :---------------------------------- | :-------------------------- |
| South Central US                    | East US 2                   |
| West Europe                         | West Europe                 |

#### Q: Can virtual users simulate pausing between test steps?

A: Yes, you can specify think times. Select a scenario in your load test and 
edit the think time in the Properties view.
 
#### Q: Where can I get more information about simulating real-world loads?

A: Learn more about how to specify 
[web performance test properties, load test scenario properties, and run settings properties](https://msdn.microsoft.com/library/ff406975.aspx).

#### Q: Can I run load tests locally and in the cloud from the same project?

A: Yes, your project can have multiple test settings files. Add another 
test settings file to your Solution Items folder. 

![Right-click test settings file, click Active Load and Web Test Settings](../_img/LoadTestMultipleTestSettings.png)
 
Now you can use one settings file to run your tests locally and the 
other settings file to run your load tests in the cloud. To switch between them, 
open the file's shortcut menu, then select the test settings file that you want to use.

#### Q: How do I install certificates or software on agents that run my load tests in the cloud?

A: In the test settings, you can use deployment options and a setup script. 
In the Deployment window, add the .exe or other files that you want to deploy on the agents. 
To install those files on the agents, use the setup script.

All the items deployed on the agents are copied to a directory on the agent. 
You can access the directory location by using %DeploymentDirectory% in the setup and cleanup script. 
For example, if you want to install WebDeploy on the agent machine, 
add WebDeploy_x64_en-US.msi to Deployment window. The setup.cmd will look like this: 

`%DeploymentDirectory%\WebDeploy_x64_en-US.msi /passive`

<a name="jmeter-tests"></a>
### Apache JMeter tests

#### Q: What is the supported JMeter version?

A: The load test agents run Apache JMeter version 2.13 only.

#### Q: Which samplers are supported?

A: Currently, only HTTP samplers are supported.

#### Q: I want to supply properties to JMeter. How do I do that?

A: Add the properties you need to a **user.properties** 
file. Upload it using the **Supporting files** parameter 
when you set up the test, and it will be applied when the load test runs.

#### Q: Are custom listeners supported?

A: Custom listeners are not currently supported.

<a name="run-monitor-tests"></a>
### Run and monitor load tests

#### Q:  Can I use mstest to run load tests with Visual Studio Team Services?

A: Yes, you can in Team Foundation Server 2015 and in Visual Studio Team Services.
For more information, see
[this blog post](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/24/cloud-load-test-support-in-mstest-exe-command-line-and-xaml-builds/).

#### Q:  Can I debug a load test while it's running in the cloud?

A: Yes, you can do this when you use Visual Studio Enterprise 2015. 
[Learn more](https://blogs.msdn.com/b/visualstudioalm/archive/2015/02/06/using-advanced-diagnostics-to-debug-issues-in-cloud-load-test.aspx).

#### Q: How can I check the status of the Cloud-based Load Testing service?

A: You can view the service status at the top of the 
[Visual Studio Team Services support page](https://www.visualstudio.com/support-overview-vs) 
and on our [service blog](http://blogs.msdn.com/b/vsoservice/). 
You can also subscribe to alerts for service status by following 
[this post in our support forum](https://social.msdn.microsoft.com/Forums/vstudio/74fdaf92-e293-4d71-bd63-cfcc8a9dcd60/subscribe-to-alerts-about-team-foundation-service-and-elastic-load-service-status).

#### Q: What are the possible load test run states?

A: When you run load tests with Visual Studio Team Services, the test run states are:

* **In-Progress**: The test run is currently running in the cloud.
* **Completed**: The test run was completed successfully.
* **Aborted**: The test run was stopped because the user clicked the stop button. 
This state can also result from issues related to your load test, 
such as issues with your test scripts.
* **Error**: The test run was stopped due to an error with the service itself. 
For example, there might be an infrastructure issue in the service, 
and it can't continue to run your test. This is not an issue caused 
by your load test or test scripts.

#### Q: Where is my load test report stored after I download it?

A: Your downloaded reports are stored in a local SQL Server Express database. 
You can 
[change the default location](http://msdn.microsoft.com/library/ms318550.aspx), 
if you want. You can also store all the reports together for everyone by changing 
the location for each user to the same database.

SQL Server Express works best for storing test results from a trial run. 
For better performance as you download more reports, use SQL Server. 
[Learn more](https://msdn.microsoft.com/library/ms182600.aspx)

#### Q: How should I view test logs after downloading the test results locally?

A: Due to a known issue, you must currently use this workaround:

1.  Start Notepad with administrator privileges.
1.  Open devenv.exe.config file. You can usually find this file at: 
    C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE
1.  Change the value of bindingRedirect to "8.0.0.0-14.0.0.0"

    ```
    <dependentAssembly>
      <assemblyIdentity name="Microsoft.VisualStudio.QualityTools.LoadTest" publicKeyToken="b03f5f7f11d50a3a" culture="neutral" />
      <bindingRedirect oldVersion="8.0.0.0-14.0.0.0" newVersion="12.0.0.0"/>
    </dependentAssembly>
    ```

<a name="troubleshooting"></a>
### Troubleshooting

#### Q: What do I do if Visual Studio stops responding when I try run a load test in the cloud?
A: To resolve this issue, see [Known issues with load testing](https://blogs.msdn.com/b/visualstudioalm/archive/2013/11/07/known-issues-with-load-testing-in-visual-studio-2013.aspx).

#### Q: How do I record a web performance test with Internet Explorer 11?

A: If the web test recorder is not active when you try and record your 
web test with Internet Explorer 11, 
see [Using Internet Explorer 11 and not able to record a web performance test](https://blogs.msdn.com/b/visualstudioalm/archive/2013/09/16/using-internet-explorer-11-and-not-able-to-record-a-web-performance-test-successfully.aspx) 
to resolve the issue.

#### Q: How do I view errors and warnings that happen when my load test is running in the cloud?

A: Status messages and test errors are reported while your load test runs. 
Status messages give you details about the load test run itself, 
such as when a connection to the results database is lost. 
Test errors relate to the test. View both these messages from the 
Details tab on the progress graphs.

![View status and error messages](../_img/LoadTestInProgress.png)

#### Q: I get an error when I try to import downloaded test results. What do I do?

A: If the error states that the connection's current state is closed, 
you can set the amount of time that a connection waits before timing out. 

Set the ConnectTimeout or Connection Timeout keywords in the connection string. 
Do not set a value of 0 as a timeout in a ConnectionString because the 
connection will keep trying to connect indefinitely.

#### Q: Why can't I use more than 250 virtual users or plug-ins when I have Visual Studio Ultimate or Visual Studio Enterprise?

A: If this happens, you must take the Visual Studio Ultimate 2013 or Visual Studio 
Enterprise 2015 Product Key from your MSDN subscription and use the "Change my Product License" 
option on the Product Information page. You must do this on every machine where you want 
to run load tests using Visual Studio Team Services. To get the product key, 
[visit this site](https://msdn.microsoft.com/subscriptions/keys/).

#### Q: Why did the REST API calls that I use stop working?

A: Starting on 26th November 2014, you must add the version 
information to your REST API calls. If your call fails with a 
**VssVersionNotSpecifiedException** exception, 
you must include **?api-version=1.0-preview.1** 
in your REST API calls. To do this, see
[Get started with the REST APIs](../../../integrate/get-started/rest/basics.md).

#### Q: I noticed that user code fails to execute if it depends on the test names. Are test names changed when run against the service?

A: When the test runs using Visual Studio Team Services, 
test names in load tests are converted to lower case. 
Any string match done on a test name by user code should 
ignore the case or convert test names to lower case.

#### Q: How do I enable client-side logs to help troubleshoot issues with load tests run in the cloud?

A: Edit devenv.exe.config with a text editor. You can usually find file at:

"C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE"

1. Add this line inside the &lt;appSettings&lt; section:

   ```
   <add key="ElsClientLogLevel" value="XXX"/>
   ```

   Where XXX can be any of the following:

   * **all** - logs all messages
   * **off** - stops logging any messages
   * **critical** - only logs critical messages
   * **error** - only logs error and critical messages
   * **warning** - logs error, critical and warning messages (default)
   * **information** - logs error, critical, warning and info messages
   * **verbose** - logs error, critical, warning, info and verbose messages

1. Add this section to the bottom of the devenv.exe.config file, 
   just above the closing tag. You can specify the path for the log 
   file by changing the initializeData value.

   ```
   <system.diagnostics>
     <trace autoflush="true" indentsize="4">
      <listeners>
       <add name="myListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="d:\VSTestHost.log"/>
      </listeners>
     </trace>
     <switches>
      <!-- You must use integral values for "value": 0 = off, 1 = error, 2 = warn, 3 = info, 4 = verbose.-->
      <add name="EqtTraceLevel" value="4" />
     </switches>
   </system.diagnostics>
   ```
                   
1. Restart Visual Studio and reproduce the issue. 
   You can then review the log file or share it with Support. You can find the log file at `%Temp%\ELSClient\`.

#### Q: Why don't I see the individual timing values in the Load Tests Results Store?

A: For Visual Studio 2013 Update 4, Visual Studio Enterprise 2015, 
and later versions, the default value for the TimingDetailsStorage property 
was changed from AllIndividualDetails to None. If you want to collect the individual timings, 
you must specifically set TimingDetailsStorage property to be AllIndividualDetails. 
See [Load Test Run Settings Properties](https://msdn.microsoft.com/library/ff406976.aspx).

<a name="errors"></a>
### Errors

#### Q: My test run failed with these errors. What do I do?

A: If you get one of these errors: 

* VS1550064
* VS1550072
* VS1550078
* VS1550081
* VS1550082
* VS1550083

[Contact Visual Studio Team Services Support](https://www.visualstudio.com/team-services/support). 
You will have to give them your test run id.

#### Q: My run was aborted because the .loadtest xml file could not be parsed. What do I do?

A: You might get these errors if you manually edit the .loadtest xml file:

* VS1550084

Open the file and revert any changes that you added. Rerun the load test. The run should complete successfully.

#### Q: Too many applications or counters were selected to run for my load test. What do I do?

A: You might get these errors if you manually edit the .loadtest xml file:

* VS1550026
* VS1550027

Open the file and revert any changes that you added. Rerun the load test. The run should complete successfully.

#### Q: No active load test settings were found in my load test. What do I do?

A: You might get this error if you close the load test wizard without completing it:

* VS1550030

To fix this problem, create another load test. Delete the failed test run.

#### Q: My load test got an error when it started or was aborted during the run. What do I do?

A: Generally, these problems happen due to issues with the cloud-based load testing service. Just try and run your load test again. If these problems still happen, contact Visual Studio Team Services support. You will have to give them your test run id.

#### Q: Where can I find information about other errors?

A: See [Visual Studio Cloud Load Testing error codes](https://blogs.msdn.com/b/visualstudioalm/archive/2014/10/21/visual-studio-cloud-load-testing-amp-error-codes.aspx) to find more details about other errors and their resolutions, where applicable.

<!-- ENDSECTION --> 

