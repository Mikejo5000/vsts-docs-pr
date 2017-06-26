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
backed by Microsoft account or Azure Active Directory (Azure AD), to protect and secure your data.  Clients 
like [Visual Studio](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#vs) and 
[Eclipse (with the Team Explorer Everywhere plug-in)](https://www.visualstudio.com/setup-admin/team-services/connect-to-visual-studio-team-services#eclipse) 
natively support Microsoft account and Azure AD authentication, so you can directly use those authentication methods 
to sign in. 

For non-Microsoft tools that integrate into Team Services but do not support Microsoft account or Azure AD authentication
interactions (for example, Git, NuGet, or XCode), you need to set up personal access tokens by using 
[Git credential managers](../../git/set-up-credential-managers.md) or by creating PATs manually (see below).  You can also use personal access tokens when there is no "pop up UI" such as with command-line tools, integrating tools or tasks into build pipelines, or using  [REST APIs](../../../integrate/get-started/rest/basics.md).

Personal access tokens essentially are alternate passwords that you create in a secure way using your normal authentication, 
and PATs can have expiration dates, limited scopes (for example, only certain REST APIs or command line operations are valid), 
and specific Team Services accounts.  You can put them into environment variables so that scripts do not hardcode 
passwords.  For more information, see [Authentication overview](../../git/auth-overview.md) and  [scopes](../../../integrate/get-started/auth/oauth.md#scopes).

[!INCLUDE [personal-access-tokens-procedure](../../git/_shared/personal-access-tokens.md)]

## Using PATs

For example using PATs, see using [Git credential managers](../../git/set-up-credential-managers.md), [REST APIs](../../../integrate/get-started/rest/basics.md), [NuGet on a Mac](../../package/nuget/consume.md#mac-os), and 
[Reporting clients](../../report/analytics/client-authentication-options.md#enter-credentials-within-a-client).
