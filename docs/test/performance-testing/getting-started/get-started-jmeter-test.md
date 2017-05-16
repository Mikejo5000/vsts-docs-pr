---
title: Apache JMeter cloud-based load testing with Visual Studio Team Services
description: Using JMeter to performance test your application in the cloud with Visual Studio Team Services
ms.prod: vs-devops-alm
ms.technology: vs-devops-test-performance
ms.assetid: 3B2A725F-4E7B-4652-BFD1-FC7C9A248B7B
ms.manager: douge
ms.author: ahomer
ms.date: 08/12/2016
---

# Run Apache JMeter load tests with Visual Studio Team Services

[!INCLUDE [version-header-ts](../../_shared/version-header-ts.md)]

Before you start:

* [Create your Visual Studio Team Services account](https://www.visualstudio.com/products/visual-studio-team-services-vs), 
  if you don't have one already.

**To run a JMeter load test:**

1. Sign in to your Visual Studio Team Services account (```https://{youraccount}.visualstudio.com```).

1. Make sure you are on the start (root) page for your account, not inside a project.
   If you are in a project, you can navigate to the account start page by using the Visual Studio icon at the left of the title bar.  

   ![Go to your account home page](_img/_shared/goto-homepage.png)

1. Go to the **Load Test** hub.

   ![From your account home page, go to Load Test](_img/_shared/LoadTestHubVSO.png)

1. If this is the first test you have created, you will see the
   "Get started with cloud-based load testing" page. 
   In the **Apache JMeter** section, choose **Create test**. 

   ![Get started page for load testing](_img/get-started-jmeter-test/JMeterLoadTestVSO-get-started.png)

   If you have previously created any tests, you will see a list of these.
   In this case, open the ![plus-icon](../../_img/plus-icon.png) &nbsp;**New**
   menu and choose **Apache JMeter test**.

   ![Start a new load test from the New menu](_img/get-started-jmeter-test/JMeterLoadTestVSO-new-menu-item.png)

1. Enter your load test parameters. To run your test near to where your users are located,
   select a closer location for your load test. Then start your test when you're ready.

   ![Add load test information, then choose Run Test](_img/get-started-jmeter-test/JMeterLoadTestVSO-parameters.png)

   >For information about the scripts and supporting files used for JMeter
   web tests, see [Build a Web Test Plan](http://jmeter.apache.org/usermanual/build-web-test-plan.html)
   on the Apache JMeter website.
 
1. As the test runs, you see live information about the progress
   of the test. You can stop the test by using the **Abort** link on the
   toolbar.

   ![Live information about the running load test](_img/get-started-jmeter-test/JMeterTestVSO-progress.png)

1. When your test is done, look at the results to see how 
   well your app performed. For example, you can see an overview
   of your app's performance in the **Summary** tab.
   This tab shows all of the main metrics such as average response
   time, user load, requests per second, failed requests, any errors
   that might have occurred, and test usage.

   ![Load test Summary tab results](_img/get-started-jmeter-test/JMeterLoadTestVSO-summary-tab.png)
 
   The lower section of the **Summary** tab shows the settings used
   for the test, and details of the five slowest requests during the test.
   If there are any transaction tests, the tab will also show the five slowest of these.
   Use the ![down arrow](_img/_shared/SimpleLoadTestVSO-sort-column.png)
   icon above a column to sort the list based on the contents of that column.

1. Open the **Charts** tab to see a graphical representation of 
   the test results over time. The charts show the average
   performance, throughput, errors, and the results of each test 
   request. Hover your mouse pointer over a chart to 
   see more details. 

   ![Load test Charts tab results](_img/_shared/LoadTestVSO-charts.png)

1. Open the **Diagnostics** tab to see detailed information such as a list
   of errors and status messages.

   ![Load test Diagnostics tab results](_img/get-started-jmeter-test/JMeterLoadTestVSO-diagnostics-tab.png)

   You can also use the ![arrow](_img/_shared/SimpleLoadTestVSO-summary-errors-icon.png)
   icon in the **Errors** section of the **Summary** tab to go directly to the 
   **Diagnostics** tab.

   ![Opening the Diagnostics tab from the Summary tab](_img/_shared/SimpleLoadTestVSO-summary-errors-link.png)

1. Open the **Logs** tab to see a list of test runs. Choose the link in
   the **Attachment** column to download the detailed log as a text file.

   ![Load test Logs tab results](_img/get-started-jmeter-test/JMeterLoadTestVSO-logs-tab.png)

1. If you have a favorite listener that you use to analyze results in
   the JMeter IDE, download the test results in .CSV format and the logs
   as a zip file from the **Download Results** link.

   ![Downloading the results and log files as a zip file](_img/get-started-jmeter-test/JMeterLoadTestVSO-download-results.png)

1. To run the same test again, choose **Rerun**.

   ![Rerunning the same test](_img/get-started-jmeter-test/JMeterLoadTestVSO-rerun-test.png)

1. Now see how you can [view and compare your load test runs](performance-reports.md).

## See also

* [Run URL-based load tests with Visual Studio Team Services](get-started-simple-cloud-load-test.md)
* [Record and replay cloud-based load tests](record-and-replay-cloud-load-tests.md)
* [Performance test your app in the cloud](getting-started-with-performance-testing.md#cloudloadtest)
* [Performance test your Azure web app under load](../app-service-web-app-performance-test.md)

[!INCLUDE[q-and-a-for-performance-testing](../../_shared/q-and-a-for-performance-testing.md)]

[!INCLUDE [help-and-support-footer](../../_shared/help-and-support-footer.md)] 
