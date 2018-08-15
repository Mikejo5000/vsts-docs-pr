---
title: Billing overview for Azure DevOps Services
description: Overview of billing management tasks in Azure DevOps Services, including how to set up billing, make purchases, and change Azure subscription for billing
ms.prod: devops
ms.technology: devops-billing
ms.assetid: d5bd13e2-aa7c-4191-aefd-bd9f05663e7b
ms.topic: overview
ms.manager: douge
ms.author: chcomley
author: chcomley
ms.date: 04/06/2018
monikerRange: 'vsts'
---


# Billing overview for Azure DevOps Services

**VSTS**

Set up billing when you need more than the **Free Tier** of resources in your Azure DevOps Services organization, or to buy other features for your users that are offered by Microsoft or other companies via the [Visual Studio Marketplace](https://marketplace.visualstudio.com/).

The Free Tier includes:

* Five Azure DevOps Services users (Basic).
* Five Package Management users.
* Free Tier of Microsoft-hosted CI/CD (one concurrent job, up to four hours per month).
* One self-hosted CI/CD concurrent job.
* 20,000 virtual user minutes of cloud-based load testing.

> During your first purchase for your Azure DevOps Services organization, you're prompt to select the Azure subscription to use for billing. The subscription can be part of your Enterprise Agreement, Pay-As-You-Go, Cloud Solution Provider (CSP), or other types of Azure subscriptions. All Azure DevOps Services services are billed via Azure. You aren't required to pay for or use any other Azure services.
> 
> These are the paid services that are offered by Microsoft:
>
> * [Azure DevOps Services users/Basic](https://marketplace.visualstudio.com/items?itemName=ms.vss-vstsuser)
> * [Microsoft-hosted CI/CD](https://marketplace.visualstudio.com/items?itemName=ms.build-release-hosted-pipelines) (formerly hosted pipelines)
> * [Self-hosted CI/CD](https://marketplace.visualstudio.com/items?itemName=ms.build-release-private-pipelines) (formerly private pipelines)
> * [Azure Test Plans Manager](https://marketplace.visualstudio.com/items?itemName=ms.vss-testmanager-web)
> * [Package Management](https://marketplace.visualstudio.com/items?itemName=ms.feed)
>
> [Cloud-based load testing](buy-load-testing-vs.md) is charged based on the load tests that you run. By default, paid usage is turned off for your Azure DevOps Services organization.
> You can only enable paid usage via the Azure portal.

## Prerequisites

The first time that you set up billing for your Azure DevOps Services organization, whether you do the setup via the Azure portal or as part of making a purchase in the Visual Studio Marketplace, you need:

* [Azure DevOps Services project collection administrator or organization owner permissions](../accounts/faq-add-delete-users.md#find-owner).
* [The **owner** or **contributor** role on your Azure subscription](add-backup-billing-managers.md).

You also need these same permissions and roles to make subsequent changes, such as changing paid quantities or adding additional paid services in your Azure DevOps Services organization.

## Next steps

* [Set up billing](set-up-billing-for-your-organization-vs.md)
* [Add a backup billing manager](add-backup-billing-managers.md)
* [Change the Azure subscription for billing](change-azure-subscription.md)

## Related articles

* [Azure DevOps Services pricing](https://azure.microsoft.com/pricing/details/visual-studio-team-services/)
* [Azure DevOps Services billing support](https://visualstudio.microsoft.com/team-services/support/)