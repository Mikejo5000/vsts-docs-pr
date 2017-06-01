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


# Permissions and access for work tracking   

<b>Team Services | TFS 2017 | TFS 2015 | TFS 2013</b> 


The team administrator role supports configuration of team settings. To be added as a team administrator, see [Configure team settings and add team administrators](../work/scale/manage-team-assets.md#add-team-admin). To learn more about stakeholder access, see [Work as a stakeholder](../work/connect/work-as-a-stakeholder.md).  

For an overview of work tracking features and functions, see [Agile tools](../work/overview.md).

<table>
<tr valign="bottom">
<th width="310px">Task</th>
<th>Stakeholders</th>
<th>Readers</th>
<th>Contributors</th>
<th>Team Admins</th>
<th width="16%">Account Owner/<br/>Project Admins</th>
</tr>
<tbody valign="top" align="center">
<tr>
<td align="left">View work items, including bugs, requirements, and tasks</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
</tr>


<tr>
<td align="left">Create and edit work items, follow a work item</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>  </td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
</tr>

<tr>
<td align="left">Change work item type </td>
<td>![checkmark](_img/checkmark.png)</td>
<td>  </td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
</tr>

<tr>
<td align="left">Move or delete work items </td>
<td> </td>
<td>  </td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
</tr>

<tr>
<td align="left">Search and query work items, save work item queries
</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>Can't save queries</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
</tr>

<tr>
<td align="left">View backlogs, boards, and plans
</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
</tr>

<tr>
<td align="left">Provide feedback
</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
</tr>

<tr>
<td align="left">Request feedback
</td>
<td> </td>
<td> </td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
</tr>

<tr>
<td align="left">Agile tools (Kanban boards, backlogs, sprint planning, portfolio management)
</td>
<td> limited interactions </td>
<td> view only</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
</tr>

<tr>
<td align="left">Configure Agile tools, set team defaults 
</td>
<td> </td>
<td> </td>
<td> </td>
<td>![checkmark](_img/checkmark.png)</td>
<td>![checkmark](_img/checkmark.png)</td>
</tr>

<tr>
<td align="left">Create new work item tags</td>
<td>Can assign existing tags</td>
<td> </td>
<td>![check mark](_img/checkmark.png)</td>
<td>![check mark](_img/checkmark.png)</td>
<td>![check mark](_img/checkmark.png)</td>

</tr>


<tr>
<td align="left">View, add, and configure Delivery Plans</td>
<td> </td>
<td>view only</td>
<td>![check mark](_img/checkmark.png)</td>
<td>![check mark](_img/checkmark.png)</td>
<td>![check mark](_img/checkmark.png)</td>

</tr>



<tr>
<td align="left">Customize project information (area paths, iteration paths, and work tracking processes) 
</td>
<td>  </td>
<td> </td>
<td>  </td>
<td>  </td>
<td>![checkmark](_img/checkmark.png)</td>
</tr>

</tbody>
</table>


<a id="grant-add-permissions"></a>  

## Grant team members additional permissions  

For teams to work autonomously, you may want to provide them with permissions that they don't have by default. Suggested tasks include providing team administrators or team leads permissions to:  

- [Create and edit child nodes under their default area path](../customize/modify-areas-iterations.md)  
- [Create and edit child nodes under an existing iteration node](../customize/modify-areas-iterations.md)  
- [Create shared queries and folders under the Shared Queries folder](../track/set-query-permissions.md).  
 
By default, team members inherit the permissions afforded to members of the team project Contributors group. Members of this group can add and modify source code, create and delete test runs, and create and modify work items. They can collaborate with other team members and [check in work to the team's code base](https://msdn.microsoft.com/library/ms181407.aspx) or [collaborate on a Git team project](../../git/get-started.md).  

![Default permissions assigned to team contributors](_img/default-permissions-assigned-to-team-contributors.png)  

If your on-premises TFS deployment includes reporting or SharePoint Products, add users to those resources. See [Add users to a team project](../../setup-admin/add-users.md). 


## Test management permissions  

Area permissions for web-based test case management and test execution control access to the following actions. 

The **Manage test suites** permission enables users to:  
<ul style="padding-left:10px">
<li style="margin-bottom:2px">Create and modify test suites</li>
<li style="margin-bottom:2px">Add or remove test cases to/from test suites</li>
<li style="margin-bottom:2px">Change test configurations associated with test suites</li>
<li style="margin-bottom:2px">Modify the suite hierarchy by moving a test suite</li>
</ul>

The **Manage test plans** permission enables users to:  
<ul style="padding-left:30px">
<li style="margin-bottom:2px">Create and modify test plans </li>
<li style="margin-bottom:2px">Add or remove test suites to or from test plans</li>
<li style="margin-bottom:2px">Change test plan properties such as build and test settings</li>
</ul>


Additional test management permissions are assigned at the team project level and include the ability to create, delete, and view test runs, and manage test configurations and environments. See [Project, object, and test-level permissions](../../setup-admin/permissions.md#project_test).  


## Related notes 

*	[Add another team](../scale/multiple-teams.md)  
*	[Set team defaults](../scale/set-team-defaults.md)  
*	[Customize iteration paths](../customize/set-iteration-paths-sprints.md)  
*	[Customize area paths](../customize/set-area-paths.md)  
*	[Configure team settings and add team administrators](../scale/manage-team-assets.md)  
*	[Set permissions and access for work tracking](../how-to/set-permissions-access-work-tracking.md) 
*	[Query by area or iteration path ](../track/query-by-area-iteration-path.md)    
