---
title: Free trials for paid Azure DevOps Services features and extensions | Azure DevOps Services
description: How to get free trials for Test Manager, Package Management, and for Azure DevOps Services extensions offered by other publishers (Azure DevOps Services, Visual Studio Online, VSO)
ms.prod: devops
ms.technology: devops-billing
ms.assetid: 435fb3a4-1766-4172-928d-80c09cfb1410
ms.topic: quickstart
ms.manager: douge
ms.author: chcomley
author: chcomley
ms.date: 04/18/2018
monikerRange: 'vsts'
---

# Quickstart: Start free trials for paid Azure DevOps Services features and extensions

[!INCLUDE [version-vsts-only](../../_shared/version-vsts-only.md)]

In this quickstart, you learn how to start a trial for your Azure DevOps Services organization and how to keep using your extension after the trial ends.

There are two paid features in Azure DevOps Services that are offered by Microsoft that you can use free for a 30-day trial:

- [Test Manager](https://marketplace.visualstudio.com/items/ms.vss-testmanager-web) (which is included on an ongoing basis for Visual Studio Enterprise, Visual Studio Test Professional, and MSDN Platforms subscribers).

- [Package Management](https://marketplace.visualstudio.com/items?itemName=ms.feed) (which is included on an ongoing basis for Visual Studio Enterprise subscribers, plus another five users in your organization).

During the trial, any user in your Azure DevOps Services organization whose access level is Basic (including Visual Studio subscribers) can use these features.
You assign these features explicitly to users within the User hub, after the trial ends. You choose to pay for a certain number of users on an ongoing basis.

This same process applies to paid extensions that are offered by other publishers within the Visual Studio Marketplace, including:

- [Timetracker](https://marketplace.visualstudio.com/items?itemName=Berichthaus.TfsTimetracker)
- [Agile Cards](https://marketplace.visualstudio.com/items?itemName=spartez.agile-cards)
- [Enhanced Export PRO](https://marketplace.visualstudio.com/items?itemName=mskold.mskold-PRO-EnhancedExport)
- [Code Quality NDepend](https://marketplace.visualstudio.com/items?itemName=ndepend.ndependextension)
- [Backlog Essentials](https://marketplace.visualstudio.com/items?itemName=agile-extensions.backlog-essentials)

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.

## Prerequisites

As the Azure DevOps Services [organization owner or project collection administrator](vsts-billing-faq.md#find-owner), you can start trials for your Azure DevOps Services organization. 
All other users can [request extensions](../../marketplace/install-vsts-extension.md).

## Start a trial for your organization

1. Sign in to [Visual Studio Marketplace > VSTS](https://marketplace.visualstudio.com/vsts).

    ![Find extension trial](_img/get-vsts-extensions/marketplace.png)

1. Find and select a paid extension that you want to try.

    ![Start the extension trial](_img/try-additional-features/mp-start-test-manager-trial.png)

1. Select your Azure DevOps Services organization to install this extension.

    ![Select your Azure DevOps Services organization for extension trial](_img/try-additional-features/select-organization.png)

1. After your extension finishes installing, go to your Azure DevOps Services organization to use your extension.

    Let your team know that they also have access.

   ![Marketplace installs your extension](_img/try-additional-features/extension-installed.png)

<a name="after-trial"></a>

## Keep your extension after the trial ends

Make sure to buy and assign the extension *before* the trial ends so that your users can continue using it without disruption. Otherwise, your users will lose access when the trial expires.
There's no penalty for buying early. Charges don't start until the trial ends.

If you lose access because the trial expired before you could purchase, buy and assign the extension like you would if you weren't doing a trial:

1. [Buy the extension](../../marketplace/install-vsts-extension.md#install-extension) for your users.

    To buy the extension, you can also go to the extension pane in your organization.

    ![User hub, extension pane](_img/try-additional-features/extension-trial-in-organization-updated-ui.png)

1. [Assign the extension](../../marketplace/assign-paid-extensions.md) to the users who need it.

## Clean up resources

To cancel a paid extension, you must have access to the Azure subscription that was used to buy it.

## Next steps

> [!div class="nextstepaction"]
> [Buy cloud-based load testing](buy-load-testing-vs.md)

## Related articles

- [Change the Azure subscription for billing](change-azure-subscription.md)
- [Azure DevOps Services pricing](https://azure.microsoft.com/pricing/details/visual-studio-team-services/)
