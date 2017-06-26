---
title: Test your Azure web app performance under load
description: Run Azure web app performance tests to check how your app handles user load. Measure response time and find failures that might indicate problems.
ms.prod: vs-devops-alm
ms.technology: vs-devops-test-performance
ms.assetid: D39BF037-ADF1-41D7-BA6D-84AADA2A16DE
ms.manager: douge
ms.author: ahomer
ms.date: 08/12/2016
---

# Performance test your Azure web app under load

[!INCLUDE [version-header-ts](../_shared/version-header-ts.md)]

Check your web app's performance before you launch it or deploy updates to production. 
That way, you can better assess whether your app is ready for release. Feel more
confident that your app can handle the traffic during peak use or at your next marketing push.

During public preview, you can performance test your app for free in the Azure Portal.
These tests simulate user load on your app over a specific time period and measure your app's response. For example, your test results show how fast your app responds to a specific number 
of users. They also show how many requests failed, which might indicate problems with your app.      

![Find performance problems in your web app](_img/app-service-web-app-performance-test/azure-np-perf-test-overview.png)

## Before you start

* You'll need an [Azure subscription](https://account.windowsazure.com/subscriptions), 
  if you don't have one already. Learn how you can 
  [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).

* You'll need a [Visual Studio Team Services (Team Services)](https://www.visualstudio.com/products/what-is-visual-studio-online-vs) 
  account to keep your performance test history. A suitable account will be created 
  automatically when you set up your performance test. Or you can create a new account 
  or use an existing account if you're the account owner. 
  [What else can I do with a Visual Studio Team Services account?](#TeamServicesAccount)

* Deploy your app for testing in a non-production environment. 
  Have your app use an App Service plan other than the plan used in production. 
  That way, you don't affect any existing customers or slow down your app in production. 

<a name="singletest"></a>
## Set up and run your performance test

1. Sign in to the [Azure Portal](https://portal.azure.com). 
   To use a Visual Studio Team Services account that you own, 
   sign in as the account owner.

1. Go to your web app.

   ![Go to Browse All, Web Apps, your web app](_img/app-service-web-app-performance-test/azure-np-web-apps.png)

1. Go to **Performance Test**.

   ![Go to Tools, Performance Test](_img/app-service-web-app-performance-test/azure-np-web-app-details-tools-expanded.png)
 
1. Now you'll link a [Visual Studio Team Services (Team Services)](https://www.visualstudio.com/products/what-is-visual-studio-online-vs) 
   account to keep your performance test history.

   If you have a Team Services account to use, select that account. If you don't, create a new account.

   ![Select existing Team Services account, or create a new account](_img/app-service-web-app-performance-test/azure-np-no-vso-account.png)

1. Create your performance test. Set the details and run the test. 
   You can watch the results in real time while the test runs.

   For example, suppose we have an app that gave out coupons at last year's holiday sale. 
   This event lasted 15 minutes with a peak load of 100 concurrent customers. 
   We want to double the number of customers this year. We also want to improve 
   customer satisfaction by reducing the page load time from 5 seconds to 2 seconds. 
   So, we'll test our updated app's performance with 250 users for 15 minutes.

   We'll simulate load on our app by generating virtual users (customers) 
   who visit our web site at the same time. This will show us how many 
   requests are failing or responding slowly.

   ![Create, set up, and run your performance test](_img/app-service-web-app-performance-test/azure-np-new-performance-test.png)

   * Your web app's default URL is added automatically. 
     You can change the URL to test other pages (HTTP GET requests only).

   * To simulate local conditions and reduce latency, 
     select a location closest to your users for generating load.

   Here's the test in progress. During the first minute, 
   our page loads slower than we want.

   ![Performance test in progress with real-time data](_img/app-service-web-app-performance-test/azure-np-running-perf-test.png)

   After the test is done, we learn that the page loads much faster 
   after the first minute. This helps identify where we might want to 
   start troubleshooting the problem.

   ![Completed performance test shows results, including failed requests](_img/app-service-web-app-performance-test/azure-np-perf-test-done.png)

## Test multiple URLs

You can also run performance tests incorporating multiple URLs
that represent an end-to-end user scenario by uploading a Visual
Studio Web Test file. Some of the ways you can create a
Visual Studio Web Test file are:

* [Capture traffic using Fiddler and export as a Visual Studio Web Test file](http://docs.telerik.com/fiddler/Save-And-Load-Traffic/Tasks/VSWebTest)
* [Create a load test file in Visual Studio](run-performance-tests-app-before-release.md)

To upload and run a Visual Studio Web Test file:
 
1. Follow the [steps above](#singletest) to open the **New performance test** blade.
   In this blade, choose the CONFIGFURE TEST USING option to open the 
   **Configure test using** blade.  

   ![Opening the Configure load testing blade](_img/app-service-web-app-performance-test/multiple-01-authoring-blade.png)

1. Check that the TEST TYPE is set to **Visual Studio Web Test** and select your HTTP Archive file.
   Use the ![folder](_img/app-service-web-app-performance-test/multiple-folder-icon.png) icon to open the file selector dialog.

   ![Uploading a multiple URL Visual Studio Web Test file](_img/app-service-web-app-performance-test/multiple-01-authoring-blade2.png)

   After the file has been uploaded, you see the list of URLs to be tested in the URL DETAILS section.
 
1. Specify the user load and test duration, then choose **Run test**.

   ![Selecting the user load and duration](_img/app-service-web-app-performance-test/multiple-01-authoring-blade3.png)

   After the test has finished, you see the results in two panes. The left pane
   shows the performnace information as a series of charts.

   ![The performance results pane](_img/app-service-web-app-performance-test/multiple-01a-results.png)

   The right pane shows a list of failed requests, with the type of error and the number
   of times it occurred.

   ![The request failures pane](_img/app-service-web-app-performance-test/multiple-01b-results.png)

1. Rerun the test by choosing the **Rerun** icon at the top of the right pane.

   ![Rerunning the test](_img/app-service-web-app-performance-test/multiple-rerun-test.png)

##  Q & A

#### Q: Why can't I see my existing Team Services account to run load tests? 

To use a Team Services account for running load tests from the Azure
portal, one of the following criteria must be satisfied:

* The account is backed by Azure Active Directory,
  [Has an Azure subscription](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-how-subscriptions-associated-directory)
  is linked to it, and the user is a member of the linked Azure subscription.

* The account is backed by [Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/)
  and the user is an owner of the account.

#### Q: Is there a limit on how long I can run a test? 

**A**: Yes, you can run your test up to an hour in the Azure Portal.

#### Q: How much time do I get to run performance tests? 

**A**: After public preview, you get 20,000 virtual user minutes (VUMs) 
free each month with your Visual Studio Team Services account. 
A VUM is the number of virtual users multipled by the number 
of minutes in your test. If your needs exceed the free limit, 
you can purchase more time and pay only for what you use.

#### Q: Where can I check how many VUMs I've used so far?

**A**: You can check this amount in the Azure Portal.

![Go to your Team Services account](_img/app-service-web-app-performance-test/azure-np-vso-accounts.png)

![Check VUMs used](_img/app-service-web-app-performance-test/azure-np-vso-accounts-vum-summary.png)

#### Q: What is the default option and are my existing tests impacted?

**A**: The default option for performance load tests is a manual test -
the same as before the multiple URL test option was added to the portal.
Your existing tests continue to use the configured URL and will work as before.

#### Q: What features not supported in the Visual Studio Web Test file?

**A**: At present this feature does not support Web Test plug-ins, data 
sources, and extraction rules. You must edit your Web Test file to remove 
these. We hope to add support for these features in future updates.

#### Q: Does it support any other Web Test file formats?
  
**A**: At present only Visual Studio Web Test format files are supported.
We'd be pleased to hear from you if you need support for other file formats. 
Email us at [vsoloadtest@microsoft.com](mailto:vsoloadtest@microsoft.com).

<a name="TeamServicesAccount"></a>
#### Q: What else can I do with a Visual Studio Team Services account?

**A**: To find your new account, go to ```https://{accountname}.visualstudio.com```. 
Share your code, build, test, track work, and ship software - all in the cloud 
using any tool or language. Learn more about how [Visual Studio Team Services](https://www.visualstudio.com/products/what-is-visual-studio-online-vs) 
features and services help your team collaborate more easily and deploy continuously.

#### Q: Can I get more detailed profiler information?

A: Yes, see [Profiling live Azure web apps with Application Insights](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler).

## See also

* [Run URL-based load tests with Visual Studio Team Services](getting-started/get-started-simple-cloud-load-test.md)
* [Run Apache JMeter load tests with Visual Studio Team Services](getting-started/get-started-jmeter-test.md)
* [Record and replay cloud-based load tests](getting-started/record-and-replay-cloud-load-tests.md)
* [Performance test your app in the cloud](getting-started/getting-started-with-performance-testing.md#cloudloadtest)
* [Profiling live Azure web apps with Application Insights](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler)

[!INCLUDE [help-and-support-footer](../_shared/help-and-support-footer.md)] 
