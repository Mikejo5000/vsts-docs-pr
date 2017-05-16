---
title: Customize the workflow | Team Services    
description: Add workflow states to a work item type for an inherited process for Visual Studio Team Services (VSTS)   
ms.technology: vs-devops-agile-wit
ms.prod: vs-devops-alm
ms.assetid: 35971F8F-26EF-4C99-9825-4AC072A6EBE4  
ms.manager: douge
ms.author: kaelli
ms.date: 03/29/2017 
---

# Customize the workflow (Inheritance process model)   

[!INCLUDE [temp](../_shared/process-feature-availability.md)]

Each work item type is associated with a workflow that supports tracking the status of work as it moves from creation to completion. To support your business and team processes, you can add custom states to most work item types (WITs). For example, you may want to insert a Triaged state for bugs, or a Design state for features or user stories. 

Here, the Bug WIT has been customized to support a Triaged state. The state and reason fields appear on the work item form in the header area.

<img src="_img/cust-workflow-form-triage-header.png" alt="Bug work item form, header area" style="border: 1px solid #CCCCCC;" /> 

##What you can customize   

You customize the workflow for a WIT by adding a custom state. Each customizable WIT consists of three or more inherited states. Inherited states differ based on the system process &mdash;[Agile](../guidance/agile-process.md), [Scrum](../guidance/scrum-process.md), or [CMMI](../guidance/cmmi-process.md)&mdash;you chose from which to create your custom process. 



<div style="float:left;width:180px;margin:3px;font-size:90%">
<p style="font-weight:bold;margin-bottom:2px;text-align:center;">![Inherited field](_img/inherited-icon.png) **Inherited states:**</p>
- [View workflow states](#hide-state)   
- [Hide a state](#hide-state)       
</div>

<div style="float:left;width:220px;margin:3px;font-size:90%">
<p style="font-weight:bold;margin-bottom:2px;text-align:center;">![Inherited field](_img/inherited-icon.png) **Custom states:**</p>
- [Add a state](#add-states)   
- [Edit a state (change color or category)](#edit-state)   
- [Remove a state](customize-process-workflow.md#remove-state)   
</div>

<div style="clear:left;font-size:100%">
</div>

<br/>

To perform any of these actions, you must be a member of the Project Collection Administrators group or be [granted explicit permissions to edit a specific process](manage-process.md#process-permissions).  

**What you can't customize**  
- You can't modify an inherited state (you can't change its name, color, or category)
- You can't hide an inherited state if it's the only one in its state category    
- You can't change the name of a custom state 
- You can't add a custom state to the Completed category
- You can't change the order of states (states are listed in the order you add them within the States page, and they're listed  alphabetically within the drop down list of a work item form)  
- You can't apply a field rule to a state (for example, make a field required)
- You can't specify a Reason for a state, instead, default reasons are defined such as Moved to state Triaged, Moved out of state Triaged 
- You can't specify allowed transitions, all transitions are defined from any state to another state (except to the Removed state).  
 
<a id="workflow-elements">  </a> 
### Workflow elements and state categories

All workflows consist of states, transitions, and reasons. A transition supports forward and backward movement among two states. When you add a custom state, the system automatically adds transitions from the custom state to all other inherited states (except for Removed).  

Each state belongs to a state category (previously referred to as a metastate). State categories support the Agile tool backlog and board views. 

<a id="workflow-states">  </a> 
#### Workflow states

Workflow states define how a work item progresses upon its creation to closure. For example, the four main states defined for the User Story (Agile process) define a progression of four states, from New, Active, Resolved, to Closed. (The Removed state supports removing a work item from appearing on the backlog; to learn more, see [Move, change, or delete work items](../backlogs/remove-delete-work-items.md#remove).)

The natural progressions and regressions of the user story, product backlog item, and requirement WITs are as shown.  

<div style="float:left;width:240px;margin:12px;font-size:90%">
<p style="font-weight:bold;padding-bottom:0px;text-align:center;">User Story (Agile)</p>
<img src="../guidance/_img/ALM_PT_Agile_WF_UserStory.png" title="User Story workflow states, Agile process " alt="User Story workflow states, Agile process" />
</div>

<div style="float:left;width:220px;margin:12px;font-size:90%">
<p style="font-weight:bold;padding-bottom:0px;text-align:center;">Product backlog item (Scrum)</p>
<img src="../guidance/_img/ALM_PT_Scrum_WF_PBI.png" title="Product backlog item workflow states, Scrum process template" style="padding-left:20px;" alt="Product backlog item workflow states, Scrum process template" />
</div>

<div style="float:left;width:220px;margin:12px;font-size:90%">
<p style="font-weight:bold;padding-bottom:0px;text-align:center;">Requirement (CMMI)</p>
<img src="../guidance/_img/ALM_PT_CMMI_WF_Requirement.png" title="Requirement workflow states, CMMI process " style="padding-left:20px;" alt="Requirement workflow states, CMMI process " />
</div>

<div style="clear:left;font-size:100%">
</div>


<a id="state-categories">  </a>  
#### State categories

State categories, on the other hand, determine how the Agile planning tools treat each workflow state. The state categories used by the backlogs and boards are Proposed, In Progress, and Complete.

Here's how the default, inherited states map to the state categories for all three system processes plus test case management WITs. The workflow states for Test Case, Test Design, and Test Suite are the same across all three system processes. 


<table valign="top" width="100%">
<tr>
<th width="30%">Categories</th>
<th width="14%">Agile</th>
<th width="14%">Scrum</th>
<th width="16%">CMMI</th>
<th width="16%">Test WITs </th>
</tr>
<tr valign="top" >
<td>**Proposed:** Assign to states associated with newly added work items that should appear on the backlog. The first column on the Kanban or task board maps to a Proposed state. </td> 
<td>New</td> 
<td>New<br/>Approved<br/>To Do (Task) </td> 
<td>Proposed<br/></td> 
<td>Design (Test Case)<br/></td> 
</tr>
<tr valign="top" >
<td>**In Progress:** Assign to states that represent active work. Work items assigned to states mapped to this category will appear in the backlog (unless you choose to hide them) and make up the middle columns on the Kanban boards. </td> 
<td>Active<br/>Resolved (Epic, Feature, User Story)</td> 
<td>Committed<br/>Open (Impediment)</td> 
<td>Active<br/>Resolved (Epic, Feature, Requirement, Task)</td> 
<td>Active (Test Plan)<br/>In Planning (Test Suite)<br/>In Progress (Test Suite)<br/>Ready (Test Case)<br/></td> 
</tr>
<tr valign="top" >
<td>**Resolved:** Assign to states that represent a solution has been implemented, but are not yet verified. Generally these states apply to bug WITs. Work items in a Resolved state appear on the backlog by default. The Agile tools treat the Resolved state category exactly the same as the In Progress state category. </td> 
<td>Resolved (Bug)</td> 
<td>n/a</td> 
<td>Resolved (Bug, Issue, Review, Risk)</td> 
<td>n/a </td> 
</tr>
<tr valign="top" >
<td>**Completed:** Assigned to states that represent work has finished. Work items whose state is in this category don't appear on the backlog and do appear in the last column of the Kanban board. Note that you can't modify states in this category nor can you add states to this category.</td> 
<td>Closed<br/></td> 
<td>Done<br/></td> 
<td>Closed<br/></td> 
<td>Closed (Test Case)<br/>Completed (Test Suite)<br/>Inactive (Test Plan)</td> 
</tr>
<tr valign="top" >
<td>**Removed:** Assigned to the Removed state. Work items in a state mapped to the Removed category are hidden from the backlog and board experiences.

<blockquote>**Note:** You should avoid using the Removed state and Removed state category as they are in the process of being deprecated.  Instead, users should Delete work items to remove them from the backlog. </td> 
<td>Removed </td> 
<td>Removed</td> 
<td>n/a</td> 
<td>n/a</td> 
</tr>
</table>  


### When to add a State versus a Kanban column

Both States and Kanban columns are used to track the status of work. Workflow states are shared across a team project while Kanban columns are shared within a team. Only project collection admins can add custom states, while team admins can add Kanban columns.  

Add custom states when you want all teams to track the status according to the business workflow adopted by the organization. By customizing the process, you automatically customize the team projects and WITs that reference that process. 

Also, by adding custom states to support those workflow states that several teams want to track, you avoid the confusion that can arise when team's create a query based on a Kanban column. Because each team can customize the Kanban board columns and swimlanes, the values assigned to work items which appear on different boards may not be the same. The primary work around for this issue is to maintain single ownership of work items by team area path. Another work around is to formalize the columns by adding custom states which can be shared across teams. 



<a id="states">  </a>
## Add a workflow state   

States you add will appear in the pick list for the States field shown in work item forms and the query editor. A transition to and from the State you add is created to every other State, except not to a Removed state. Also, default reasons are defined, such as Moved to state Triaged, Moved out of state Triaged.

<a id="open-process-wit">  </a>
### Open Process>Work Item Types in the admin context

To customize the workflow for a WIT, you must work from the admin context Process hub. 

You can open the admin context Process hub from a work item form or by choosing the Account Settings option from the gear option. For details, see [Customize a process, Start customizing](customize-process.md#start-customizing).

>[!IMPORTANT]  
>If you don't see the Account settings option, then you are working from an on-premises TFS. The Process page isn't supported. You must use the features supported for the On-premises XML process model as described in [Customize your work tracking experience](../customize/customize-work.md).
	
<a id="add-states"></a>
### Add a state 

>[!NOTE]  
>States that you add to the task WIT will add columns to the task board. If you [track bugs along with tasks](../customize/show-bugs-on-backlog.md), then states you add to the bug WIT will also add columns to the task board. You don't have to add the same states to each of these WITs, however, you may want to do so in order to  update the status in the same way and to minimize the number of columns that get added.  
>
>If you add a state to a WIT which you is associated with a backlog level, each team will need to update their [Kanban board columm settings](../kanban/add-columns.md) in order to view and use the affected Kanban board.  


0. From the Work Item Types tab, choose the work item type you want to modify, choose States, and then choose New State.    

	<img src="_img/cpworkflow-add-state.png" alt="Process page, Bug WIT, States tab, Add state" style="border: 1px solid #CCCCCC;" />  

0. Enter the name of the State, choose its category and color, and then click Save. The color you specify will appear throughout the product including on the work item form and when the State field appears on a backlog, boards, query results, and more.  

	<img src="_img/cpw-new-state-triaged.png" alt="State dialog box" style="border: 1px solid #CCCCCC;" />  
	
0. When you've finished adding states for the WIT, verify your changes by refreshing your browser and open a work item of the type you just customized. 

	Here we show the state drop down field with Triaged selected. 

	<img src="_img/cpw-added-triage-state-in-form.png" alt="Bug form, Triaged state added" style="border: 1px solid #CCCCCC;" /> 

0. Remember, when you add a state to a WIT which is associated with a backlog level, each team that uses the Kanban board will need to [update their column settings](../kanban/add-columns.md).

<a id="edit-state"></a>
### Edit a state

You can edit the category or the color of a custom state. However, you can't change the name of the custom state. 

0. Choose Edit from the &hellip; context menu for the state you want to modify.  
  
	<img src="_img/cpworkflow-edit-state.png" alt="Bug WIT, Edit custom state" style="border: 1px solid #CCCCCC;" /> 

0. Modify the category or color, and then click Save. 

0. If you change the category, teams that use the Kanban board to update their status will need to update their [column settings](../kanban/add-columns.md).    
 
<a id="remove-state"></a>
## Hide or remove a state

When you hide or remove a state:  
- The state no longer appears in the State pick list for the WIT
- No changes occur to the work item history     
- Existing work items maintain their state value, but are in an invalid state. If you want to make a change to the work item, you must first update the state values. You may want to create a query and do a bulk update to move the affected work items into a valid state. If you add the state back to the work item type, the work items revert to a valid state.  
 

<a id="hide-state"></a>
### Hide or unhide an inherited state 

You can hide an inherited state that your team doesn't use in its workflow process. However, you must have at least one state defined for each category. 

0. Open the &hellip; context menu for the state you want to hide and choose the **Hide** option. 

	Here we hide the Resolved state for the Bug WIT. 

	<img src="_img/cpworkflow-hide-state.png" alt="Hide an inherited state" style="border: 1px solid #CCCCCC;" /> 

	>[!NOTE]  
	>If you hide the state of a WIT tracked on a Kanban board, each team  that uses the Kanban board will need to [update their column settings](../kanban/add-columns.md).

0. To unhide, open the &hellip; context menu and choose the **Unhide** option.  
 

<a id="remove-state"></a>
### Remove a custom state 
0. Open the &hellip; context menu for the state you want to remove, and choose **Remove**. You can only remove a custom state.     

0. From the Remove State dialog, click Remove.   

	<img src="_img/workflow-remove-state-warning.png" alt="Remove state warning dialog box" style="border: 1px solid #CCCCCC;" />  

0.  If teams use the Kanban board to update their status, each team will need to update their [column settings](../kanban/add-columns.md).    
 

## Related notes  

As you customize a workflow, all team projects that reference the inherited process that you're customizing will automatically update to reflect the customized workflow states. To view your customizations, refresh your web browser.  

Additional topics of interest:  

- [Add or modify a work item type](customize-process-wit.md)
- [Customize a field](customize-process-field.md)  
- [Customize a form](customize-process-form.md)
- [Customize a process](customize-process-field.md) 
- [Add or edit Kanban columns](../kanban/add-columns.md)  
- [Query by workflow or Kanban board changes](../track/query-by-workflow-changes.md)    

[!INCLUDE [temp](../_shared/help-support-shared.md)]

[!INCLUDE [temp](../_shared/custom-help.md)]

<!---
UPDATE CONTENT FOR THIS FWLINK: http://go.microsoft.com/fwlink/?LinkId=286303. 

Requested and Accepted States - Code Review Request and Code Review Response  

Rules governing States 
All work item types need at least 2 statesone Proposed/In Progress state and one Completed state.

-->
 










