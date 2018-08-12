---
title: Buy and manage cloud service provider customer VSTS subscriptions
description: Cloud service provider (CSP) partners can purchase and manage Visual Studio Team Services (VSTS) for their customers
ms.prod: devops
ms.technology: devops-billing
ms.assetid: a7d8ce85-c95f-495a-82f3-9237b49b29de
ms.topic: conceptual
ms.manager: douge
ms.author: chcomley
author: chcomley
ms.date: 01/22/2018
monikerRange: 'vsts'
---
# Buy VSTS resources for your customers

[!INCLUDE [version-vsts-only](../../../_shared/version-vsts-only.md)]

Partners in the cloud service provider (CSP) program can purchase [Visual Studio Team Services (VSTS) resources](https://visualstudio.microsoft.com/team-services/pricing) for
their customers, including VSTS users (who get Basic  features), Test Manager, Package Management, Private Pipelines, and
Hosted Pipelines.

## Prerequisites

To set up billing for a customer who's already created a VSTS organization by using a Microsoft account identity
(in other words, not an identity in their Azure Active Directory), the customer needs to do the following steps first:

1. Your customer must [change their VSTS organization to be backed by their Azure Active Directory](../../accounts/access-with-azure-ad.md).
2. Your customer must [unlink the existing Azure subscription that's used for billing on their VSTS organization](../change-azure-subscription.md), if they had previously set up billing.

Make sure your identity hasn't been added into the customer's Azure Active Directory. If it has, you need to have the identity removed before you can go through the purchasing steps for your customer.

## Buy resources for customers

<iframe src="//channel9.msdn.com/Shows/Visual-Studio-for-CSP-Partners/CSP-How-to-buy-VSTS/player" width="600" height="315" allowFullScreen="true" frameBorder="0"></iframe>

1. Sign in to the [Partner Center](https://partnercenter.microsoft.com).
2. Choose the customer for whom you're purchasing.
3. Choose **Service Management**.
4. Choose **Visual Studio Marketplace**
5. Make sure you're in the VSTS tab, and then search for and choose **VSTS Users**.
6. Select **Get** and move through the purchase process. Choose the VSTS organization that needs more users. Choose the Azure subscription to bill for the purchase. Enter the number of users that your customer needs. Review the order and complete it.

You can buy other items the same way. After choosing **Visual Studio Marketplace**, search for **Test Manager**, **Package Management**, **Hosted Pipelines**, and so on.
