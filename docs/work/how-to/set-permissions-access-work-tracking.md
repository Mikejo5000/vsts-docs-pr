---
title: Set permissions and access for tracking  | VSTS & TFS
description: How to guide for setting permissions and access levels to support work tracking tasks (Visual Studio Team Services and Team Foundation Server)
ms.technology: vs-devops-agile-wit
ms.prod: vs-devops-alm
ms.assetid: 5AD0BF62-C91E-46DD-8C1A-C8D1F8F8D05F
ms.manager: douge
ms.author: kaelli
ms.topic: get-started-article  
ms.date: 06/01/2016
---


# Set permissions and access for work tracking   

<b>Team Services | TFS 2017 | TFS 2015 | TFS 2013</b> 

 

<a id="set-permissions" >  </a> 

## Set permissions to restrict access to work items   

Permissions placed on an area paths allows you to permit or restrict access to edit or modify work items, test cases, or test plans assigned to those areas. You can restrict access to users or groups. You can also set permissions for who can add or modify areas or iterations for the team project.  

1. Open the **Security** dialog for the node you want to manage.  

	![Open the security dialog](../customize/_img/ALM_CW_OpenSecurityDialog.png)

2. Select the group or team member, and then change the permission settings. For example, for the Disallow Access Group, deny the ability to view, modify, or edit work items in the FabrikamFiber area path.

	![Permissions for an area node](../customize/_img/ALM_CW_PermisionsForArea.png)

	If the group or team member doesn't appear in the list, you can [**Add** it](../../setup-admin/add-users.md).  
	
You can specify two explicit authorization states for permissions: **Deny** and **Allow**. In addition, permissions can exist in one of three additional states.  

| Permission 		| Authorization |
| ----------------- | ------------- |
| Allow 			| Explicitly grants users to perform the task associated with the specific permission. For users to access a task, the associated permission must be set to **Allow** or **Inherited allow**. |
| Deny 				| Explicitly prevents users from performing the task associated with the specific permission. **Deny** takes precedence over **Allow**. <br/>For exceptions to these rules, see [Permissions reference](../../setup-admin/permissions.md#inheritance)|
| Inherited allow/Inherited deny 	| Allows or denies a user to perform the task associated with the permission based on the permission set for a group to which the user belongs. |
| Not set         	| Implicitly prevents users from performing the action associated with the permission. <br/>Because the permission is neither explicitly set to **Deny** nor explicitly set to **Allow**, authorization for that permission can be inherited from other groups of which the user or group is a member. <br/>By default, most permissions are not set to either **Deny** or **Allow**, the permissions are left **Not set**.  |


For additional ways to restrict modifications to work items, see [Restrict who can create or modify a work item](../reference/apply-rule-work-item-field.md). 



## Related notes 

*	[Add another team](../scale/multiple-teams.md)  
*	[Set team defaults](../scale/set-team-defaults.md)  
*	[Customize iteration paths](../customize/set-iteration-paths-sprints.md)  
*	[Customize area paths](../customize/set-area-paths.md)  
*	[Configure team settings and add team administrators](../scale/manage-team-assets.md)  
*	[Set permissions and access for work tracking](../how-to/set-permissions-access-work-tracking.md) 
*	[Query by area or iteration path ](../track/query-by-area-iteration-path.md)    
