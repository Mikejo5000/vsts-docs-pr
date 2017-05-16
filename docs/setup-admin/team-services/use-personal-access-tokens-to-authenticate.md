---
title: Authenticate access with personal access tokens | Visual Studio Team Services & TFS
description: Use personal access tokens to authenticate access to Visual Studio Team Services and Team Foundation Server (TFS)
ms.topic: get-started-article
ms.prod: vs-devops-alm
ms.technology: vs-devops-setup
ms.assetid: d980d58e-4240-47c7-977c-baaa7028a1d8
ms.manager: douge
ms.author: estfan
ms.date: 08/08/2016
---

# Authenticate access with personal access tokens for Team Services and TFS

**Team Services** | **TFS 2017**

Visual Studio Team Services and Team Foundation Server use enterprise-grade authentication, 
backed by Microsoft account or Azure Active Directory (Azure AD), 
to protect and secure your data.
Clients like [Visual Studio](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#vs) and 
[Eclipse (with the Team Explorer Everywhere plug-in)](https://www.visualstudio.com/setup-admin/team-services/connect-to-visual-studio-team-services#eclipse) 
natively support Microsoft account and Azure AD authentication, 
so you can directly use those authentication methods to sign in. 

Other clients like Git, NuGet, and Xcode, 
require basic credentials in the form of a username and password, 
and don't support Microsoft account and Azure AD features like multi-factor authentication. 
For these clients, set up personal access tokens 
by using [Git credential managers](../../git/set-up-credential-managers.md). 
You can also use personal access tokens with command-line tools and to access 
[REST APIs for Team Services and TFS](../../../integrate/get-started/rest/basics.md).

If you don't want to use a credential manager, 
you can manually create personal access tokens. 
You can limit a token's use to a specific lifetime, 
a Visual Studio Team Services account, 
and [scopes](../../../integrate/get-started/auth/oauth.md#scopes) 
of activities that this token authorizes.

[!INCLUDE [personal-access-tokens-procedure](../../git/_shared/personal-access-tokens.md)]
