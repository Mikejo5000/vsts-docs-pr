---
title: Add a team, add team members | Team Services & TFS 
description: Add another team or a hierarchy of teams to scale your Agile tools--product and sprint backlogs, Kanban and task boards     
ms.technology: vs-devops-agile-wit
ms.prod: vs-devops-alm
ms.assetid: 9F1D0A0F-02D5-4E06-A5EC-C220472A0F66
ms.manager: douge
ms.author: kaelli
ms.date: 04/06/2017
---



# Add teams and team members  

<b>Team Services | TFS 2017 | TFS 2015 | TFS 2013 </b>  

Adding a team is the #1 way in which Agile tools supports a growing organization. Once your team grows beyond its optimum size&mdash;typically anywhere from 6 to 9 members&mdash;you might consider moving from a one team structure to a two team structure. For enterprises adopting Agile tools, setting up a hierarchical team structure provides several advantages to portfolio and program managers to track progress across several teams.  

[!INCLUDE [temp](../_shared/image-differences.md)]  





<a id="add-team"> </a>  
## Move from one team to two teams 
As your team grows, you can easily move from one team to two. In this example, we add two feature teams, Email and Voice, and maintain the Fabrikam Fiber team with visibility across each of these two teams.  

### Add two feature teams 

Add and configure two teams, Email and Voice. Here we show you how to add and configure the Email team. 

1.	From the web portal, click the ![gear settings icon](../_img/icons/gear_icon.png) icon to open the administration page for the team project.  

	![Open team project admin page](../connect/_img/ALM_CAL_OpenAdminPage.png)  

	If you're not a project administrator, [get added as one](../../setup-admin/add-administrator-tfs.md). Only project administrators can add teams.  

2.	Create a new team. Give the team a name, and make sure to select **Create an area path with the name of the team**.

	![Create a sub-team with its own area path](_img/scale-agile-add-new-team-co.png)

	If you do not select this option, you will have to set the default area path for the team once you create it. You can choose an existing area path or create a new one at that time. Team tools aren't available until the team's default area path is set.

3.	Select the team from the Overview tab to configure it. 

	<img src="_img/scale-agile-select-team-to-configure-it-co.png" alt="Web portal, admin context, team project, Overview page, Select a sub-team to configure it" style="border: 1px solid #CCCCCC;" /> 

5.	To select the set of sprints the team will use, open the **Iterations** page for the team. See [Set team defaults, Select team sprints and default iteration path](set-team-defaults.md#activate).    

	If your team isn't listed in the top navigation row, open the Overview tab, select your team, and then return to the Iterations tab.

4.	To change the area paths that the team will reference, open the **Areas** page. See [Set team defaults, Set team default area path(s)](set-team-defaults.md#team-area-paths).     

<a id="add-team-members"> </a>  

###Add team members
If you're moving from one team to two teams, team members already have access to the team project. If you're setting up a team structure for the first time, adding user accounts as team members provides them access to the team project and team assets. Access to the team project is required to support sharing code and planning and tracking work. 

Several Agile tools, like capacity planning and team alerts, are team-aware. That is, they automatically reference the user accounts of team members to support planning activities or sending alerts. 

1.	From the Overview tab for your team, add a user account.  

	<img src="_img/scale-agile-add-team-account.png" alt="Web portal, admin context, team project, Overview page, Add a Windows user or group account" style="border: 1px solid #CCCCCC;" /> 

	>[!NOTE]  
	>If you use Team Services, see [Add team members](../../setup-admin/team-services/add-team-members-vs.md). The steps are similar but slightly different.  

2.	Enter the sign-in addresses or display name for each account you want to add. Add them one at a time or all at the same time.  

	The first time an account is added to TFS, you must enter the full domain name and the alias. Afterwards, you can browse for that name by display name as well as account name. To learn more, see [Set up groups for use in TFS deployments](../../setup-admin/tfs/admin/setup-ad-groups.md).  

	![Type the account aliases and check name](_img/scale-agile-add-team-members-user-accounts.png)  

	>[!TIP]  
	>You must enter user and group names one at a time. However, after entering a name, the account is added to the list, and you can type another name in the Identities text box before choosing to save your changes.   

3.	Now these users are members of the Email team. You can always return to this page to add or remove members. 

	<img src="_img/agile-scale-manage-team-members.png" alt="Web portal, admin context, team project, Overview page, Manage team members" style="border: 1px solid #CCCCCC;" /> 

	To add an account as a team administrator, see [Configure team settings and add team administrators](manage-team-assets.md). 

4.	(On-premises TFS only) As a last step, send the team URL to newly added team members so they can start contributing to the team. For example:  
	
	Email team: ```http://fabrikamfiber:8080/tfs/DefaultCollection/Fabrikam%20Fiber/Email```   
	Voice team: ```http://fabrikamfiber:8080/tfs/DefaultCollection/Fabrikam%20Fiber/Voice```   


### Move work items under teams 
Now that your two feature teams are configured, you'll want to move existing work items from their current assignments to the team's default area path. This way, the work items will show up on each feature team's backlog. 

1.	The quickest way to do this, is to [create a query](../track/using-queries.md) of all work items you want to reassign, multi-select those items belonging to each team, and [bulk edit the area path](../backlogs/bulk-modify-work-items.md). 

	<img src="_img/scale-agile-bulk-modify-area-path-co.png" alt="Web portal, Queries page, Bulk modify select work items" style="border: 1px solid #CCCCCC;" /> 

2.	After you bulk modify, do a bulk save. 
 
	<img src="_img/scale-agile-bulk-save-area-path-co.png" alt="Web portal, Queries page, Bulk save selected work items" style="border: 1px solid #CCCCCC;" /> 

<a id="include-area-paths"> </a>  

### Configure the default team project  
One last step in moving from one team to two teams requires configuring the default team project to exclude sub-areas.  

1. Open the Areas tab administration page for the team project, and change the setting as shown.  

	<img src="_img/multiple-teams-exclude-sub-area-paths.png" alt="Web portal, Admin context, default team project, Exclude work items defined in sub-area paths" style="border: 1px solid #CCCCCC;" /> 

2.	Refresh the product backlog page for the team, and you'll see only those work items assigned to the Fabrikam\Account Management area path.  

	<img src="_img/multiple-teams-product-backlog-default-team.png" alt="Web portal, Backlog view of default team" style="border: 1px solid #CCCCCC;" /> 

<a id="grant-add-permissions"></a>  

## Grant team members additional permissions  

For teams to work autonomously, you may want to provide them with permissions that they don't have by default. Suggested tasks include providing team administrators or team leads permissions to:  

- [Create and edit child nodes under their default area path](../customize/modify-areas-iterations.md)  
- [Create and edit child nodes under an existing iteration node](../customize/modify-areas-iterations.md)  
- [Create shared queries and folders under the Shared Queries folder](../track/set-query-permissions.md).  
 
By default, team members inherit the permissions afforded to members of the team project Contributors group. Members of this group can add and modify source code, create and delete test runs, and create and modify work items. They can collaborate with other team members and [check in work to the team's code base](https://msdn.microsoft.com/library/ms181407.aspx) or [collaborate on a Git team project](../../git/get-started.md).  

![Default permissions assigned to team contributors](_img/default-permissions-assigned-to-team-contributors.png)  

If your on-premises TFS deployment includes reporting or SharePoint Products, add users to those resources. See [Add users to a team project](../../setup-admin/add-users.md). 



##Try this next 

Once you've created a team, you'll want to configure your Agile tools to support how your team works. Also, consider adding one or more accounts as team administrators. Team admins have the necessary permissions to add team members, add a team picture, and [configure and manage all team assets](manage-team-assets.md).  

If team members don't have access to all the features they want, check that they have [the access level needed for those features](../connect/change-access-levels.md).  

### Stakeholder access  
By granting users a Stakeholder license or adding them to the [Stakeholder access level](../connect/work-as-a-stakeholder.md), you enable them to create and modify work items that they create. Stakeholders can report code defects, suggest a product feature, or further annotate their feedback responses.


## Delete a team 

1. To delete a team, open the team project admin context, open the &hellip; context menu for the team you want to delete, and choose the **Delete** option.   

	<img src="_img/multiple-teams-delete-team.png" alt="Web portal, admin context-team project level, Delete team" style="border: 1px solid #CCCCCC;" />  

	You must be a member of the Project Administrators group or be [granted explicit permissions to edit project information](../../setup-admin/permissions.md#edit-team-project-level-information-permission) to delete a team project. 
 
	>[!IMPORTANT]   
	>Deleting a team deletes all team configuration settings, including team dashboards, backlogs, and boards. Data defined for work items assigned to the team are left unchanged. Once deleted, you can't recover the team configurations. 

2. To complete the delete operation, you must type the name of the WIT as shown. 

	<img src="_img/multiple-teams-delete-team-confirmation-dialog.png" alt="Delete team confirmation dialog" style="border: 1px solid #CCCCCC;" />  
 


## Related notes

From a specific team admin page, you can rename a team or change the team description. Here are a few other topics related to working with teams: 
 
- [Configure team settings, add team administrators](manage-team-assets.md)  
- [Visibility across teams](visibility-across-teams.md)  
- [Review team plans](review-team-plans.md)    
- [Track work when contributing to several teams](capacity-planning.md)
- [Scaled Agile Framework](scaled-agile-framework.md)   
- [Practices that scale](practices-that-scale.md) 
- [Restrict access to select features and functions](../../setup-admin/restrict-access-tfs.md)   



