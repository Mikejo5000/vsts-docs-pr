---
title: Pay for more team services | Visual Studio Team Services
description: Buy more capacity for builds, releases, or cloud-based load testing in Visual Studio Team Services (Visual Studio Online, VSO, VSTS)
ms.topic: get-started-article
ms.prod: vs-devops-alm
ms.technology: vs-devops-admin
ms.assetid: 3f42a1b2-1a32-440a-bf43-61006c59c5bf
ms.manager: douge
ms.author: estfan
ms.date: 1/10/2017
---

#  Buy more capacity for builds, releases, or cloud-based load testing in Visual Studio Team Services

**Team Services**

Visual Studio Team Services offers these
[additional team services](https://www.visualstudio.com/team-services/pricing):

* [**Build & Release**](../../build/concepts/licensing/concurrent-pipelines-ts.md):
Create, queue, and monitor cross-platform builds and releases with these task-based services.
Use Hosted Pipelines to run builds and deploy releases concurrently on Microsoft-managed
agents. Use Private Pipelines to run builds and deploy releases on machines that you manage,
running agent software from Microsoft.
  
  > To better connect with Release Management, **Build & Deployment** was renamed **Build & Release**.  
  > Unit names are now **Hosted Pipelines** and **Private Pipelines**, rather than Hosted Agents and Private Agents.
  
  Each pipeline lets you run 1 build or deploy 1 release at a time.
  The maximum number of concurrent builds that you can run and releases
  that you can deploy at the same time is limited only by the number of pipelines that you have.

  Your Team Services account includes these **free** amounts:

  * 1 free Hosted Pipeline

    With this free Hosted Pipeline, you get 4 hours (240 minutes) per month
    and a maximum duration of 30 minutes per build or deployment.
    If you just need more build time for 1 concurrent build or release,
    [buy another Hosted Pipeline](#buy-build-release) without the 4-hour limit
    to increase your maximum duration per build or deployment up to 6 hours.
    For more concurrent builds or releases, [buy more Hosted Pipelines](#buy-build-release).

  * 1 free Private Pipeline

    With this free Private Pipeline, run unlimited concurrent builds
    or deploy 1 release at a time in Team Foundation Server 2017,
    or run 1 build or deploy 1 release at a time in Team Services on
    agent software from Microsoft.  Private agents are now free and unlimited.
    In TFS, each Visual Studio Enterprise subscriber also contributes
    a Private Pipeline that you can use. You can also
    [buy more Private Pipelines](#buy-build-release).

  Learn about:

    * Team Services: Build & Release pipelines](../../build/concepts/licensing/concurrent-pipelines-ts.md)
    * TFS: Build & Release pipelines](../../build/concepts/licensing/concurrent-pipelines-tfs.md)
    * Pricing for Build & Release pipelines](https://www.visualstudio.com/team-services/pricing)


*  **Build (XAML)**: The hosted XAML build controller is no longer supported.
Accounts created on or after April 2016 do not have access to it.
We plan to remove the hosted XAML build controller from all accounts,
possibly as soon as March 2017.

  > **Important:** If you have an account where you still need to run [XAML builds](https://msdn.microsoft.com/en-us/library/ms181709%28v=vs.120%29.aspx),
  > you should set up an [on-premises build server](https://msdn.microsoft.com/en-us/library/ms252495%28v=vs.120%29.aspx)
  > and switch to an [on-premises build controller](https://msdn.microsoft.com/en-us/library/ee330987%28v=vs.120%29.aspx) now.
  > If you used the hosted XAML build controller, you might have been paying for build minutes, which is a model we no longer support.
  > Please purchase concurrent pipelines. See [Buy pipelines for Build & Release](#buy-build-release).
  > We will soon block the hosted pool from using the per-minute billing model.
  > By making this switch, you can run longer builds (unlimited minutes within reason).

*  [**Cloud-based Load Testing**](../../test/performance-testing/index.md):
Create load tests using Visual Studio Ultimate 2013, Visual Studio Enterprise 2015, or later.
Run those tests in Visual Studio Team Services. Load tests are measured and billed
in virtual user minutes (VUM). For an explanation see
[this Q&A](../../test/performance-testing/getting-started/get-started-simple-cloud-load-test.md#VUM). 

  Your Visual Studio Team Services account includes **free**
  20,000 virtual user minutes per month for cloud-based load testing.
  If you need more than this amount, you must first
  [set up billing for your Team Services account](set-up-billing-for-your-account-vs.md).
  You can then [buy more Cloud-based Load Testing](#buy-load-testing) in the
  [Azure classic portal](https://manage.windowsazure.com/) or the [Azure portal](https://portal.azure.com).

<a name="buy-build-release"></a>
##  Buy more pipelines for Build & Release

Before you start:

*  You'll need Team Services
[project collection administrator or account owner permissions](#FindOwnerPCA)
to purchase for your Team Services account.

*  You'll need an Azure subscription that you can
link to your Team Services account for billing,
if your Team Services account isn't linked already.
[Which Azure subscriptions can I use?](#AzureMSDNSubscription)

  To use an existing Azure subscription for billing,
  you'll need at least Co-administrator permissions for that subscription.
  If you don't have permissions, have an Azure Account
  Administrator or Service Administrator
  [add you as Co-administrator to the Azure subscription that you want to use for billing](set-up-billing-for-your-account-vs.md#AddAzureAdmin).

  If you don't have an Azure subscription,
  you can create a subscription when you start your purchase.
  Or [create your Azure subscription here before you start](https://account.windowsazure.com/subscriptions/).
  You'll get the necessary administrator permissions
  with your new subscription.

  Your Team Services account will reuse this Azure subscription
  when you make future purchases for your Team Services account
  from the [Visual Studio Marketplace](https://marketplace.visualstudio.com)
  or from Azure. [More about Azure subscriptions for billing](#billing).

### Buy pipelines

> **Note** If you previously bought agents in the Azure portal, they're now pipelines,
> but don't worry, your monthly purchases and pricing won't change.
> If you need to change the number of pipelines that you're buying each month,
> please go to the Visual Studio Marketplace.
> We plan to retire the experience for buying agents in the Azure portal soon.


0.  As Team Services project collection administrator or account owner,
sign in to either:

  *  [**Visual Studio Marketplace** > **Build and release** > **Hosted pipelines for Build and Release**](https://marketplace.visualstudio.com/items?itemName=ms.build-release-hosted-pipelines)
  *  [**Visual Studio Marketplace** > **Build and release** > **Private pipelines for Build and Release**](https://marketplace.visualstudio.com/items?itemName=ms.build-release-private-pipelines)<p/>

0.  Choose **Buy** for your selected pipeline.

  <img alt="Select your Team Services account" src="./\_img/get-more-build-load-testing/buy-hosted-build-release-pipelines.png" style="border: 1px solid #CCCCCC" />

0.  Select your Team Services account,
if you have multiple accounts.

  <img alt="Select your Team Services account" src="./\_img/get-more-build-load-testing/select-team-services-account.png" style="border: 1px solid #CCCCCC" />

  <p><a data-toggle="collapse" href="#expando-why-no-ts-account">Don't see your Team Services accounts? &#x25BC;</a></p>
  <div class="collapse" id="expando-why-no-ts-account">
  <p>To select your Team Services account here, you must have have Team Services
  [project collection administrator or account owner permissions](#FindOwnerPCA).
  </div>

0.  Confirm the Azure subscription that you'll use for billing.

  If you have multiple Azure subscriptions,
  select the Azure subscription that you want to use.
  Or if you don't have an Azure subscription,
  create a new subscription now to use for billing.
  [More about Azure subscriptions for billing](#billing)

  <img alt="Confirm or select your Azure subscription" src="./\_img/get-more-build-load-testing/select-azure-subscription.png" style="border: 1px solid #CCCCCC" />

  <p><a data-toggle="collapse" href="#expando-why-no-azure-sub">Don't see the Azure subscription that you expect? &#x25BC;</a></p>
  <div class="collapse" id="expando-why-no-azure-sub">
  <p>To use an existing Azure subscription for billing,
  you'll need at least Co-administrator permissions for that subscription.
  If you don't have permissions,
  have an Azure Account Administrator or Service Administrator
  [add you as a Co-administrator to the linked Azure subscription](set-up-billing-for-your-account-vs.md#AddAzureAdmin).
  </div>

0.  Select the number of pipelines that you want to buy.
Finish your purchase.

  <img alt="Select number of pipelines to buy" src="./\_img/get-more-build-load-testing/select-number-hosted-pipelines.png" style="border: 1px solid #CCCCCC" />

0.  To view your pipelines, go to your Team Services account.

  <img alt="View pipelines in your Team Services account" src="./\_img/get-more-build-load-testing/confirm-hosted-pipeline-purchase.png" style="border: 1px solid #CCCCCC" />

  <img alt="Go to Team Services account toolbar > Build and Release" src="./\_img/get-more-build-load-testing/manage-pipelines-team-services.png" style="border: 1px solid #CCCCCC" />

  To return to the Build & Release hub in
  your Team Services account at any time,
  go to your Team Services account toolbar,
  then go to **Build and Release**
  (```https://{youraccount}.visualstudio.com/_admin/_buildQueue?_a=resourceLimits```).

<a name="change-paid-pipelines"></a>
### Change your purchased pipelines

When your team's needs for build or release capacity changes,
you can update the number of pipelines that you bought.

0.  Go to your Team Services account toolbar,
then go to **Build and Release**
(```https://{youraccount}.visualstudio.com/_admin/_buildQueue?_a=resourceLimits```).

  <img alt="Go to Team Services account toolbar > Build and Release" src="./\_img/get-more-build-load-testing/manage-pipelines-team-services.png" style="border: 1px solid #CCCCCC" />

0.  Choose **Change purchased quantity**
for the paid pipeline that you want to update,
so you can go to the Visual Studio Marketplace.

0.  In the Visual Studio Marketplace,
choose **Buy**, select your Team Services account,
then update your number of paid pipelines.

<a name="buy-load-testing"></a>
## Buy more Cloud-based Load Testing

Before you start:

*  You'll need Team Services
[project collection administrator or account owner permissions](#FindOwnerPCA)
to purchase for your Team Services account.

*  You must first
[set up billing for your Team Services account](set-up-billing-for-your-account-vs.md),
if you haven't already. You'll need an [Azure subscription](#AzureMSDNSubscription)
that you can link to your Team Services account for billing.

*  If you're going through the Azure portal, you'll also need at least
[Co-administrator permissions](set-up-billing-for-your-account-vs.md#AddAzureAdmin)
for the Azure subscription that's linked to your Team Services account for billing.

You can follow the steps below for the Azure classic portal
or the Azure portal. Both portals will give you the same results.

<div style="background-color: #f2f0ee;padding-top:10px;padding-bottom:10px;">
<ul class="nav nav-pills" style="padding-right:15px;padding-left:15px;padding-bottom:5px;vertical-align:top;font-size:18px;">
<li style="float:left;" data-toggle="collapse" data-target="#buy-load-testing"></li>
<li style="float: right;"><a style="max-width: 374px;min-width: 120px;vertical-align: top;background-color:#AEAEAE;margin: 0px 0px 0px 8px;min-width:90px;color: #fff;border: solid 2px #AEAEAE;border-radius: 0;padding: 2px 6px 0px 6px;outline-style:none;height:32px;font-size:14px;font-weight:400" data-toggle="pill" href="#azure-classic-portal-0">Azure classic portal</a></li>
<li class="active" style="float: right"><a style="max-width: 374px;min-width: 120px;vertical-align: top;background-color:#007acc;margin: 0px 0px 0px 0px;min-width:90px;color: #fff;border: solid 2px #007acc;border-radius: 0;padding: 2px 6px 0px 6px;outline-style:none;height:32px;font-size:14px;font-weight:400" data-toggle="pill" href="#azure-portal-0">Azure portal</a></li>
</ul>

<div id="buy-load-testing" class="tab-content collapse in fade" style="background-color: #ffffff;margin-left: 15px;margin-right:15px;padding: 5px 5px 5px 5px;">
<div id="azure-portal-0" class="tab-pane fade in active">
<p>**Azure portal**
<p>
<ol>
<li>[Sign in to the Azure portal](https://portal.azure.com/).
<p>If you experience browser problems with Azure,
make sure that you use a [supported browser](https://azure.microsoft.com/en-us/documentation/articles/azure-preview-portal-supported-browsers-devices/).
<li>Go to **More services** > **Developer tools** > **Team Services accounts**.
Select your Team Services account.
<p>
<p><img alt="Browse, Team Services accounts, select your account" src="./_img/_shared/AP_VSO_SelectLinkedAccount.png" style="border: 1px solid #CCCCCC" />
<p>
<p>[Why don't I see my Team Services account?](#WhyNoVSOAccount)
<p>
<li>Select **Cloud-based load testing**.
<p>
<p><img alt="Click Settings, select Clouse-based load testing" src="./_img/get-more-build-load-testing/AP_VSO_ManageServices.png" style="border: 1px solid #CCCCCC" />
<p>
<li>Turn on paid load testing.
<p>
<p>If you want, set a monthly limit on the virtual user minutes that you use.
When you're done, save your changes.
<p>
<p><img alt="Click Paid, select an optional monthly limit, save changes" src="./_img/get-more-build-load-testing/AP_VSO_PaidCloudLoadTesting.png" style="border: 1px solid #CCCCCC" />
<p>
</ol>
</div>

<div class="tab-pane fade" id="azure-classic-portal-0" style="background-color: #ffffff;margin-left: 15px;margin-right:15px;padding: 5px 5px 5px 5px;">
<p>**Azure classic portal**
<p>
<ol>
<li>[Sign in to the Azure classic portal](https://manage.windowsazure.com/)
as your Azure subscription Co-administrator.
<p>
<p>If you experience browser problems with Azure,
make sure that you use a [supported browser](https://azure.microsoft.com/en-us/documentation/articles/azure-preview-portal-supported-browsers-devices/).
<p>
<li>Select your Team Services account.
<p>
<p><img alt="Select your Team Services account" src="./_img/_shared/AzureChooseLinkedAccount.png" style="border: 1px solid #CCCCCC" />
<p>
<p>[Why don't I see my Team Services account?](#WhyNoVSOAccount)
<p>
<li>Go to **Scale**.
<p>
<p><img alt="Click Scale" src="./_img/_shared/AzureScaleLicensesResources.png" style="border: 1px solid #CCCCCC" />
<p>
<li>Turn on paid Load Testing.
You can also set monthly limits on the amounts that your account uses.
<p>
<p>You're not charged until your account goes above the free monthly amounts.
<p>
<p><img alt="Turn on paid Load Testing. Select optional monthly limits" src="./_img/get-more-build-load-testing/AzureManageResources.png" style="border: 1px solid #CCCCCC" />
<p>
<li>When you're done, save your changes.
<p>
<p><img alt="Save changes" src="./_img/_shared/save-changes.png" style="border: 1px solid #CCCCCC" />
<p>
<p>To check the amounts used by your account,
you can come back to the Azure classic portal.
<p>
<p><img alt="Check amounts used on your account dashboard in Azure" src="./_img/get-more-build-load-testing/AzureDashboard.png" style="border: 1px solid #CCCCCC" />
<p>
</ol>
</div>


</div></div>

####  Next

*  [Build your app](../../build/apps/index.md)
*  [Load test your app](../../test/performance-testing/getting-started/get-started-simple-cloud-load-test.md)

## Q & A
<!-- BEGINSECTION class="md-qanda" -->
####Q:  Why pay for pipelines?

A:  When you pay for pipelines, you can run more than one build or release at the same time
in your Team Services account. Learn
[about pipeline pricing](https://www.visualstudio.com/team-services/pricing)
or [how pipelines work](../../build/concepts/licensing/concurrent-pipelines-ts.md).

#### Q: Are there any limits on builds, releases, and load testing?

A: Yes, there's a limit on the duration for each build, deployment, or test run.

For Build & Release, your free hosted pipeline includes 4 hours per month
for builds and releases with a maximum duration of 30 minutes per build or deployment.
A paid hosted pipeline increases your maximum duration to 6 hours per build or deployment.

For Cloud-based Load Testing, the limit depends on where you're running your test.
For details, see [this Q&A](../../test/performance-testing/getting-started/get-started-simple-cloud-load-test.md#test-limits).

<a name="AzureMSDNSubscription"></a>

[!INCLUDE [azure-subscriptions-for-billing](../../_shared/qa-azure-subscriptions-for-billing.md)]

<a name="billing"></a>

[!INCLUDE [azure-billing](../../marketplace/_shared/qa-azure-billing.md)]

#### Q:  When do I get billed?

A:  You're charged only for services used above the free monthly limits.
Your charges are prorated during the 1st month. After that,
you're billed automatically on the 1st day of the calendar month.

*  Free minutes reset on the 1st of the month.

*  Each paid hosted pipeline or private pipeline
includes unlimited minutes per month, within reason.

*  Each connected private XAML controller is counted as one private pipeline,
although a private XAML controller can host more than one agent.

*  For Cloud-based Load Testing, you're charged for each 
   [virtual user minute](../../test/performance-testing/getting-started/get-started-simple-cloud-load-test.md#VUM).

*   Graduated discounts Cloud-based Load Testing
are calculated based on your Azure subscription billing cycle.

Learn more about [pricing here](https://www.visualstudio.com/team-services/pricing).

#### Q: Are there other ways to get features for my account?

A: Yes, you can add other features to your Team Services account when you
[download and install extensions from the Visual Studio Marketplace](https://www.visualstudio.com/get-started/marketplace/get-vsts-extensions).

<a name="no-accounts"></a>

[!INCLUDE [no-accounts](../../marketplace/_shared/qa-no-accounts.md)]

<a name="WhyNoVSOAccount"></a>

[!INCLUDE [azure-why-no-team-services-account](../../_shared/qa-azure-why-no-team-services-account.md)]

<a name="FindOwnerPCA"></a>

[!INCLUDE [find-project-collection-administrator](../../_shared/qa-find-project-collection-administrator.md)]

[!INCLUDE [find-account-owner](../../_shared/qa-find-account-owner.md)]

<a name="get-support"></a>

[!INCLUDE [azure-account-billing-support](../../_shared/qa-azure-account-billing-support.md)]

[!INCLUDE [get-team-services-support](../../_shared/qa-get-team-services-support.md)]

<!-- ENDSECTION -->
