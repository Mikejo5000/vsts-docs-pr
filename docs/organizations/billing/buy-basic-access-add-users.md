---
title: Buy Basic access for your VSTS users in the Marketplace
description: Steps for how to buy more or increase VSTS users when you need more than the free amount via the Visual Studio Marketplace
ms.prod: devops
ms.technology: devops-billing
ms.assetid: 02cb8774-6d1d-4f15-8818-b56541033b1f
ms.topic: quickstart
ms.manager: douge
ms.author: chcomley
author: chcomley
ms.date: 08/02/2018
monikerRange: 'vsts'
---

# Quickstart: Pay for VSTS users (Basic)

[!INCLUDE [version-vsts-only](../../_shared/version-vsts-only.md)]

In this quickstart, you learn how to pay for more users in your VSTS organization. You only need to pay for users when your team size exceeds the free limits. It's free to add users who have a [Visual Studio subscription](https://visualstudio.microsoft.com/team-services/pricing/). You also get five additional users free in your VSTS organization.

[Pay for additional VSTS users](https://marketplace.visualstudio.com/items?itemName=ms.vss-vstsuser) in whatever quantity you need. When you pay for VSTS users, the total number of users that you can add as members in your organization increases. This amount is added to the free limits previously mentioned.

For a list of included features, see the [feature comparison](https://visualstudio.microsoft.com/team-services/compare-features/).

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.

## Prerequisites

The first time that you set up billing for your VSTS organization, whether you do the setp up via the Azure portal or as part of making a purchase in the Visual Studio Marketplace, you need:

* [VSTS project collection administrator (PCA) or organization owner permissions](../accounts/faq-add-delete-users.md#find-owner). If you aren't a PCA or organization owner, you're prompted to send a purchase request to the admins for your VSTS organization.

   > [!div class="mx-imgBorder"]
![Non-project admin submit request](_img/buy-more-basic-access/non-organization-admin-purchase-request.png)

* [The **owner** or **contributor** role on your Azure subscription](add-backup-billing-managers.md).

To make subsequent edits to paid quantities in your VSTS organization, you need only the owner or contributor role on your Azure subscription.

<a name="buy-access-vs-marketplace"></a>

## Increase the number of paid VSTS users on your organization

1. Sign in to [**Visual Studio Marketplace** > **Other** > **VSTS Users**](https://marketplace.visualstudio.com/items?itemName=ms.vss-vstsuser) and choose **Get**.

   > [!div class="mx-imgBorder"]
![Go to Visual Studio Marketplace, Other, VSTS Users](_img/buy-more-basic-access/marketplace-choose-get-vsts-users.png)

2. Select your VSTS organization (if you have multiple organizations) and then choose **Buy**.

   > [!div class="mx-imgBorder"]
![Select your organization](_img/buy-more-basic-access/marketplace-choose-buy.png)

3. Confirm the Azure subscription where your VSTS charges are billed and then choose **Continue**.

   If you have multiple Azure subscriptions, select the Azure subscription that you want to use. If you don't have an Azure subscription, you can create a new one.

   > [!div class="mx-imgBorder"]
![Confirm or select your Azure subscription](_img/buy-more-basic-access/marketplace-confirm-subscription.png)

4. Enter the number of paid VSTS users and then choose **Continue**. You also see the number of free users that are included, which is separate.

   > [!div class="mx-imgBorder"]
![Enter the number of paid VSTS users](_img/buy-more-basic-access/marketplace-select-number-of-users.png)

5. Review your order and then choose **Confirm**.

   > [!div class="mx-imgBorder"]
![VSTS Marketplace review and confirm order](_img/buy-more-basic-access/marketplace-choose-confirm.png)

6. Choose **Manage users** to go to your VSTS organization and [add new users](../accounts/add-organization-users-from-user-hub.md).

The number of users to whom you can assign Basic appears on the right side of your screen.

   > [!div class="mx-imgBorder"]
![Number of users to whom you can assign Basic](_img/buy-more-basic-access/vsts-manage-users.png)

## Clean up resources

To remove users or make an adjustment, sign in to VSTS. Choose **Manage users** and then choose **Change quantity**.

## Next steps

> [!div class="nextstepaction"]
> [Buy CI/CD](buy-more-build-vs.md#prerequisites)

## Related articles

* [Reduce or cancel paid VSTS users](reduce-cancel-paid-vsts-users.md)
