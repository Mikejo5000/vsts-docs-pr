---
title: Billing frequently asked questions (FAQ) 
description: Find answers to frequently asked questions about billing for your Azure DevOps Services organization, which is managed in the Azure portal
ms.prod: devops
ms.technology: devops-billing
ms.assetid: 62d94b8a-256a-4347-905a-3393f5d8a13f
ms.topic: conceptual
ms.manager: douge
ms.author: chcomley
author: chcomley
ms.date: 06/13/2018
monikerRange: 'vsts'
---

# Azure DevOps Services billing FAQ

[!INCLUDE [version-vsts-only](../../_shared/version-vsts-only.md)]

Make sure to review [Azure DevOps Services pricing](https://azure.microsoft.com/pricing/details/visual-studio-team-services//) and the [Azure DevOps Services billing overview](overview.md) to start.

You have to set up billing when you need more than the *free tier* of resources in your Azure DevOps Services organization: 

* 5 Azure DevOps Services users (Basic)
* 5 Package Management users
* Free tier of Microsoft-hosted continuous integration/continuous development (CI/CD) (1 concurrent job, up to 4 hours per month)
* 1 self-hosted CI/CD concurrent job
* 20,000 virtual user minutes of cloud-based load testing 

You also have to set up billing to buy other features (for your users) that are offered by Microsoft or by other companies via the [Visual Studio Marketplace](https://marketplace.visualstudio.com/).

### Q: Can I buy Azure DevOps Services by using a purchase order?

A: No. Azure DevOps Services must be purchased through an Azure subscription. (Think of it as your Azure billing account.)

### Q: What types of Azure subscriptions can be used to buy Azure DevOps Services?

A: Almost all Azure subscriptions can be used. We support Azure subscriptions connected to your
[Enterprise Agreement (EA)](https://azure.microsoft.com/pricing/enterprise-agreement/), Azure subscriptions set up by
Cloud Solution Providers (CSPs), Azure subscriptions set up through Microsoft Open License resellers, and Pay-As-You-Go Azure subscriptions. You can even buy using Azure subscriptions that Visual Studio subscribers set up as a subscriber benefit. (But no, you can't use your monthly credit to pay for more Visual Studio subscriptions.)

The only notable exclusion is that you can't use the [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).

### Q: Can I use the monthly Azure credits from my Visual Studio subscription to buy Azure DevOps Services?

A: No, you can't use the monthly Azure credits from [Visual Studio subscriptions](https://visualstudio.microsoft.com/products/subscriber-benefits-vs)
to pay for Azure DevOps Services. Before you make purchases by using this type of Azure subscription, you must [remove your spending limit](https://azure.microsoft.com/pricing/spending-limits/).

<img alt="Spending limit" src="_shared/_img/spending-limit.png" style="border: 1px solid #CCCCCC" />

<a name="spending-limit"></a>

> [!NOTE]
> Remove your spending limit indefinitely. This prevents disabling your Azure subscription when your recurring monthly charges are billed the next month.
> Otherwise, all resources billed to this subscription will be suspended, including virtual machines and all other workloads.

<img alt="Remove spending limit indefinitely" src="_shared/_img/remove-spending-limit.png" style="border: 1px solid #CCCCCC" />

### Q: Am I required to buy other Azure services?

A: Not at all. If you only want to buy Azure DevOps Services via Azure, you can do that.

### Q: Can tags be applied to Azure DevOps Services organizations from the Azure portal?

A: No, but this feature is in our backlog to add in the future.

## Enterprise Agreement customers

### Q: Can I use an Enterprise Agreement to buy Azure DevOps Services?

A: Yes, you can. You'll need to be an owner or contributor for an Azure subscription that was created for your EA. Be sure to make your purchases for Azure DevOps Services directly in the Visual Studio Marketplace. You cannot purchase Azure DevOps Services by using a purchase order. 

### Q: How can I tell whether I have the necessary privileges to buy services in the Visual Studio Marketplace through my organization's Enterprise Agreement?

A: The easiest approach to determine if you have the right privileges is to select the **Buy** button for a service offered in the Visual Studio Marketplace. You need to select an Azure subscription (which is a billing account) from a presented list of Azure subscriptions that are currently linked to your sign-in. Because the name of the Azure subscription defaults to the type of billing account (for example, "Pay-As-You-Go" or "Enterprise Agreement"), it's often clear if the Azure subscription is part of your Enterprise Agreement.

Another approach is to try to visit the [Azure Enterprise Portal](http://ea.azure.com). If you can reach it successfully, then you already have either the enterprise admin or the organization owner role. Only organization owners can set up new Azure billing in an Enterprise Agreement. 

If you can't access the Azure Enterprise Portal, inquire within your organization to find out who your Enterprise Admin is, and ask that person to add you as an organization owner within the Azure Enterprise Portal. If you can't find this person, you can [submit a support ticket](http://aka.ms/AzureEntSupport) and request the contact information. You need your organization's name and your Enterprise Agreement enrollment number for the support ticket.

### Q: Can I use the Azure Monetary Commitment funds from my Enterprise Agreement to buy Azure DevOps Services?

A: Yes, you can use these prepaid funds for all Azure DevOps services that Microsoft offers. Make sure to choose an Azure subscription that was created for your EA when you [set up billing for your Azure DevOps Services organization](set-up-billing-for-your-organization-vs.md).

The only exclusion is for Azure DevOps Services extensions offered by partners in the Visual Studio Marketplace. These charges will appear on your next "overage" invoice. Typically this happens monthly, but due to historical rules for some EA customers, an overage invoice might not be issued for several months. Please consult a licensing specialist for your EA if you need to know what amount of additional purchases (purchases that are not eligible for Azure Monetary Commitment funds) will trigger an overage invoice.

## How charges are processed

### Q: How are user charges (Azure DevOps Services User/Basic, Test Manager, and Package Management) and CI/CD concurrent job charges (for both Microsoft-hosted and self-hosted CI/CD) processed?

A: At the first purchase, we bill a prorated quantity to cover the remaining days in the current month. For instance, if a purchase of 10 Test Manager users happens on April 15, then we charge 5 units because 50% of the month remains (15 days of a 30-day month). On the first of May, and each month thereafter until you cancel, the full 10 units will be billed.

When you increase the paid quantity later, we also prorate the increased units to cover the remaining days in the current month. So if you buy 1 more Test Manager user on May 10, we would bill roughly 0.677 units (21 days remaining in the 31-day month of May). 

### Q: How do reductions or cancellations work?

A: When you reduce or cancel user charges or CI/CD charges, you're canceling automatic renewal. The features and/or CI/CD capacity continue through the end of the current calendar month, taking effect on the fist day of the next month.

## Changes in Azure subscription status

### Q: What happens if I cancel my Azure subscription or my credit card expires?

A: When the Azure subscription used for billing on your Azure DevOps Services organization is not in active status - for example, because you cancel it or the credit card used for billing expires - your Azure DevOps Services organization will revert to the free tier of service. But you'll keep any paid users or paid CI/CD concurrent jobs until next month.

>[!NOTE]
>You must keep your Azure subscription in good standing to avoid interruptions in paid Azure DevOps services.

### Q: Where can I check my bill or update billing details on my Azure subscription?

A: If you're the owner or contributor for the Azure subscription used for billing your Azure DevOps Services organization, you can view your billing details in the [Azure portal](https://account.azure.com/).

## Other questions

### Q: Why is my Azure DevOps Services organization already linked to an Azure subscription?

A: This happens if someone already set up billing for your Azure DevOps Services organization, either through the Azure portal or while purchasing something for this organization via the
[Visual Studio Marketplace](https://marketplace.visualstudio.com/vsts). Each Azure DevOps Services organization can use only one Azure subscription for billing. Charges cannot be split across multiple Azure subscriptions.

### Q: Can I use the same Azure subscription for billing across multiple Azure DevOps Services organizations?

A: Yes, you can use the same Azure subscription for billing across multiple Azure DevOps Services organizations. But you can't link a single Azure DevOps Services organization to multiple Azure subscriptions.

<a name="find-owner"></a>

### Q: How do I find a project collection administrator?

A: You can find your [project collection administrator](../security/set-project-collection-level-permissions.md) in your Azure DevOps Services organization's security settings.

1. Go to your Azure DevOps Services organization's security settings.

   <img alt="Click gear button, Security" src="../../_shared/_img/organization-settings-new-ui.png" style="border: 1px solid #CCCCCC" />

2. Under **Security**, view your project collection administrators.

   <img alt="Go to Project Collection Administrators, Members" src="../../_shared/_img/collection-manage-security-groups-new-ui.png" style="border: 1px solid #CCCCCC" />

### Q: How do I find the organization owner?

A: You can find the current owner in your Azure DevOps Services organization settings.

1. Go to your Azure DevOps Services organization settings.

    <img alt="Go to organization settings" src="../../_shared/_img/organization-settings-new-ui.png" style="border: 1px solid #CCCCCC" />

2. Under **Settings**, find the current owner.

    <img alt="Find current owner" src="../../_shared/_img/organization-owner-new-ui.png" style="border: 1px solid #CCCCCC" />

### Q: Can I buy Azure DevOps Services from my software reseller?

A:  Yes you can, if your reseller participates in the Cloud Solution Provider program. Just ask them.

## Buy Azure DevOps Services now

* [Azure DevOps Services Users/Basic](https://marketplace.visualstudio.com/items?itemName=ms.vss-vstsuser)
* [Microsoft-hosted CI/CD](https://marketplace.visualstudio.com/items?itemName=ms.build-release-hosted-pipelines) (formerly hosted pipelines)
* [Self-hosted CI/CD](https://marketplace.visualstudio.com/items?itemName=ms.build-release-private-pipelines) (formerly private pipelines)
* [Test Manager](https://marketplace.visualstudio.com/items?itemName=ms.vss-testmanager-web)
* [Package Management](https://marketplace.visualstudio.com/items?itemName=ms.feed)

## Related articles

* [Set up billing](set-up-billing-for-your-organization-vs.md)
* [Add backup billing managers](add-backup-billing-managers.md)
* [Change the Azure subscription for billing](change-azure-subscription.md)
* [Azure DevOps Services pricing](https://azure.microsoft.com/pricing/details/visual-studio-team-services/)
* [Azure DevOps Services billing support](https://visualstudio.microsoft.com/team-services/support/)
