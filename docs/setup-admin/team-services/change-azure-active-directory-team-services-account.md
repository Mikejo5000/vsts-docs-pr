---
title: Team Services - Change Azure AD | Visual Studio Team Services
description: Team Services - Change directory (tenant) in Azure Active Directory (Azure AD, AAD) for Visual Studio Team Services (VSTS, Visual Studio Online, VSO)
ms.prod: vs-devops-alm
ms.technology: vs-devops-admin
ms.assetid: c687302d-ca34-44ea-8cfb-88fe7330072d
ms.manager: douge
ms.author: estfan
ms.date: 08/04/2016
---

#	Team Services: Change Azure Active Directory (Azure AD) tenant

**Team Services**

To move your Visual Studio Team Services account 
between directories (tenants) in Azure AD, 
disconnect your account from its current directory, 
then reconnect your account to the directory that you want.

<a name="permissions"></a>

You'll need:

*	Team Services account owner permissions. Only account 
owners can manage directory connections. 
[How do I find the account owner?](#find-owner)

*	At least Basic access, not Stakeholder

*	Global administrator permissions 
for your source and target Azure AD directories (tenants). 
Learn [how to manage Azure AD administrators](https://azure.microsoft.com/en-us/documentation/articles/active-directory-assign-admin-roles/).

*	Co-administrator permissions for the Azure subscriptions 
associated with your source and target directories. 
Learn [how to manage Azure subscription administrators](set-up-billing-for-your-account-vs.md#AddAzureAdmin).

*	A temporary Microsoft account, like @outlook.com, 
to move your Team Services account between directories. 
This Microsoft account will need these permissions, 
which you'll set up below:

	*	Source directory global administrator
	*	Target directory user administrator
	*	Azure subscription Co-administrator for both directories
	*	Team Services account owner. Only account owners can change directory connections.

##	What happens to current users?

Your work in Team Services is associated with your sign-in address. 
During directory migration, all Team Services account users need
Microsoft accounts to sign in. They'll continue working seamlessly 
if their Microsoft accounts share the same sign-in addresses that they use now. 
Otherwise, they'll lose access until you finish the migration or 
unless you add them as new users to your Team Services account.

After migration, users must be members of the target directory 
to get access to your Team Services account. They'll continue 
working seamlessly if they use the same sign-in addresses that they use now. 
Otherwise, you'll have to add them as new users to your Team Services account. 
Your organization might have policies about adding external users to the directory, 
so find out more first.

##	Prepare your source directory

You'll now set up source directory permissions and Team Services account owner permissions
so you can perform the migration.

###	Set up your Microsoft account as Azure subscription co-administrator

0.	Sign in to the [Azure classic portal](https://manage.windowsazure.com)
as the source directory global administrator.

	To change your Azure AD, you must use the Azure classic portal.

	[Why am I asked to choose between my work or school account and my personal account?](#ChooseOrgAcctMSAcct)

0.	Go to your Azure subscription settings.

	![Settings, Administrators, Add](./_img/_shared/azure-ad-add-subscription-coadmin1.png)

0.	Add your Microsoft account as the Azure subscription Co-administrator. Save your changes.

	![Add subscription co-administrator](./_img/_shared/azure-ad-add-subscription-coadmin2.png)

###	Set up your Microsoft account as global administrator in your source directory

0.	In Azure, identify the directory that's connected to your Team Services account.

	![Identify connected directory](./_img/manage-work-access/AzureFindConnectedDirectory.png)

0.	Find and select that source directory.

	![Select your directory](./_img/manage-work-access/AzureChooseAD.png)

0.	Add your Microsoft account to the source directory.

	![View directory members](./_img/manage-work-access/AzureAddMembers1.png)

	![Add Microsoft account to source directory](./_img/manage-work-access/AzureAddMembers2.png)

0.	Give global administrator permissions to your Microsoft account. Save your changes.

	![Add your Microsoft account](./_img/_shared/azure-ad-add-user.png)

	![Select global admin](./_img/_shared/azure-ad-add-global-admin.png)

###	Set up your Microsoft account as your Team Services account owner

0.	Sign in to your Team Services account (```http://{youraccount}.visualstudio.com```) as the account owner. 

	[Why am I asked to choose between my work or school account and my personal account?](#ChooseOrgAcctMSAcct)

0.	View your Team Services account users.

	![Users hub](./_img/_shared/users-hub-jamal.png)

0.	Add your Microsoft account to your Team Services account as a user.

	![Add your Microsoft account](./_img/change-azure-active-directory/add-msa-vsts.png)

	Your Microsoft account appears in this list 
	because you added this user to the source directory.

0.	Sign in to your Team Services account with your Microsoft account,
so that Team Services can validate this user. Otherwise, 
your Microsoft account won't appear in the possible account owners list.

0.	Sign back in to your Team Services account as the account owner. 
Now change the Team Services account owner to your Microsoft account. 
Learn [how to change Team Services account owners](change-account-ownership-vs.md).

	**Important**: Before you disconnect your Team Services account,
	make sure that this Microsoft account is the Team Services account owner. 

##	Prepare your target directory

Now you'll set up target directory permissions for your Microsoft account 
to continue performing the migration. You'll also add your Team Services 
account users to the target directory, if they're not members already, 
so they can get Team Services account access as directory members.

###	Set up your Microsoft account as Azure subscription Co-administrator

0.	Sign in to the [Azure classic portal](https://manage.windowsazure.com)
as the target directory global administrator.

0.	Go to your Azure subscription settings.

	![Settings, Administrators, Add](./_img/change-azure-active-directory/azure-add-subscription-target-coadmin1.png)

0.	Add your Microsoft account as the Azure subscription Co-administrator. Save your changes.

	![Add subscription co-administrator](./_img/change-azure-active-directory/azure-add-subscription-target-coadmin2.png)

###	Set up your Microsoft account as a user administrator in the target directory

0.	Find and select the directory that you want connected to your Team Services account.

	![Find target directory](./_img/change-azure-active-directory/azure-choose-target-directory.png)

0.	Add your Microsoft account to that target directory.

	![View directory members](./_img/change-azure-active-directory/azure-add-members-target1.png)

	![Add Microsoft account to target directory](./_img/change-azure-active-directory/azure-add-members-target2.png)

0.	Add your Team Services account users to the target directory, if they're not members already. 
Learn how to [manage users in Azure AD](https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/).

0.	Give user administrator permissions to your Microsoft account. Save your changes.

	![Add your Microsoft account](./_img/_shared/azure-ad-add-user.png)

	![Select user administrator](./_img/_shared/azure-ad-add-admin-user-role.png)

##	Migrate your Team Services account between directories

###	Disconnect your Team Services account from the source directory

0.	Sign in to the [Azure classic portal](https://manage.windowsazure.com) 
with the Microsoft account that you're using for the migration.

0.	Select your Team Services account.

	![Select your Team Services account](./_img/manage-work-access/AzureSelectConnectedVSO.png)

0.	Configure your account.

	![Configure your account](./_img/manage-work-access/azure-configure-disconnect.png)

0.	Disconnect your account from the source directory.

	![Disconnect account](./_img/manage-work-access/AzureDisconnectDirectory1.png)

	![Select None, no directory connection](./_img/manage-work-access/AzureDisconnectDirectory2.png)

	After you save your changes, your Team Services account is disconnected. 
	Now, only users with Microsoft accounts can sign in to your Team Services account. 
	This is why we previously set up your Microsoft account as a Team Services account user.

	![Your account is now disconnected](./_img/manage-work-access/AzureDisconnectDirectory3.png)

0.	Unlink your Team Services account from the source Azure subscription.

	![Select your Team Services account](./_img/_shared/azure-unlink-subscription.png)

	Your Team Services account is removed from the Azure classic portal. 
	You can now link your account to another Azure subscription and directory.

###	Connect your Team Services account to the target directory

0.	Link your Team Services account to the target Azure subscription.

	![Link Team Services account](./_img/set-up-billing/AzureDeveloperServicesStart.png)

	![Select your Team Services account and target Azure subscription](./_img/change-azure-active-directory/select-account-subscription.png)

0.	Configure your account.

	![Configure your account](./_img/manage-work-access/azure-configure-disconnect.png)

0.	Connect your account to the target directory. Save your changes when you're done.

	![Connect your Team Services account](./_img/manage-work-access/AzureDisconnectDirectory3.png)

	![Select target directory](./_img/change-azure-active-directory/select-directory.png)

0.	To check that you finished this task successfully, invite a user from the target directory 
to your Team Services account. Confirm that they can sign in. Learn how to 
[add users and assign access](add-account-users-assign-access-levels-team-services.md).

0.	Add the remaining users from the target directory to your Team Services account.

0.	If you use tools that run outside a web browser, like the Git command line tool, 
then your alternate credentials for those tools won't work anymore. 
You must [set up your credentials](http://support.microsoft.com/kb/2991274/en-us)
again for the Team Services account that you connected.

###	Reassign Team Services account ownership to a directory member

0.	Sign in to your Team Services account (```https://{youraccount}.visualstudio.com```) 
with the Microsoft account that you used for the migration.

0.	Reassign ownership for your Team Services account to a directory member.
Learn [how to change Team Services account owners](change-account-ownership-vs.md).

0.	Remove the Microsoft account that you used for the migration
from your source and target Azure subscriptions and directories.

## Q&A

<!-- BEGINSECTION class="md-qanda" -->

####Q:	Why don't I see the directory that I want to connect? What do I do?

A:	This might happen because:

*	You don't have [administrator permissions](#permissions) 
to manage directory connections.

*	You don't have a 
[valid "full" Azure subscription](https://azure.microsoft.com/en-us/pricing/purchase-options/), 
like a "Pay-As-You-Go" subscription, associated with the directory 
that you want to use. This typically happens with Office 365 Azure AD.

*	Your Team Services account isn't linked to the Azure subscription 
associated with your directory.

Learn [how to resolve why you can't see your directory](manage-organization-access-for-your-account-vs.md#why-not-my-directory).

<a name="find-owner"></a>

[!INCLUDE [find-account-owner](../../_shared/qa-find-account-owner.md)]

[!INCLUDE [why-no-owned-accounts](../../_shared/qa-why-no-owned-accounts.md)]

<a name="ChooseOrgAcctMSAcct"></a>

[!INCLUDE [choose-msa-azuread-account](../../_shared/qa-choose-msa-azuread-account.md)]

[!INCLUDE [choose-msa-azuread-account2](../../_shared/qa-choose-msa-azuread-account2.md)]

[!INCLUDE [why-cant-sign-in-msa-azuread-account](../../_shared/qa-why-cant-sign-in-msa-azuread-account.md)]

<a name="get-support"></a>

[!INCLUDE [get-team-services-support](../../_shared/qa-get-team-services-support.md)]

<!-- ENDSECTION --> 
