---
title: About process customization and inherited processes 
titleSuffix: Codex Agile
description: Describes what an inherited process is and how you use it to customize the work tracking system and Agile tools for a Codex Agile project 
ms.technology: devops-agile
ms.prod: devops
ms.assetid: 
ms.manager: douge
ms.author: kaelli
ms.topic: conceptual 
monikerRange: 'vsts'
ms.date: 07/10/2018
---




# About process customization and inherited processes  

[!INCLUDE [temp](../../_shared/codex-agile.md)]

<a id=" inherited "> </a> 

To customize the work tracking system for a Codex project, you *customize* an inherited process. All Codex projects that use the inherited process, inherit the customizations made to that process. On the other hand, you *configure* your [Agile tools&mdash;Scrum and Kanban&mdash;through the web UI](../about-teams-and-settings.md).

There are a number of customizations you can make. The primary ones are adding custom fields, adding custom work item types (WITs) or modifying an existing WIT. 
<a id="what-you-can-customize">  </a>
Below you'll find an index to those tasks you can perform to customize an inherited process.  Some options of inherited elements are locked and can't be customized.  

## System versus inherited processes 

You'll see two types of processes:

- ![locked icon](_img/process/locked-icon.png) System processes &mdash;[Scrum, Agile, and CMMI](../../work/work-items/guidance/choose-process.md)&mdash;which are locked from being changed.   
- ![inherited process icon](_img/process/inherited-process-icon.png) Inherited processes, which you can customize, are so named as they inherit from the system process from which they were created. Any updates VSTS makes to the parent system process will automatically update your custom inherited process.  

In addition, all processes are shared. That is, one or more team projects can use a single process. Instead of customizing a single team project, you customize a process. Changes made to the process automatically update all team projects that use that process. 

Once you've created an inherited process, you can customize it, create team projects based on it, make a copy of it, and change existing team projects to use it. 

For example, as shown in the picture below, you see a list of team projects defined for the *fabrikam* account. The second column shows the process used by each team project. To update the *Fabrikam Fiber* team project, you need to update the *MyAgile* process (which inherits from the Agile system process). Any changes you make to the *MyAgile* process will also update the *Test Agile* team project. You can't customize the *Scrum project*, on the other hand, until you change it to a Scrum inherited process.

<img src="_img/process/mprocess-overview-project-list.png" alt="Admin context, Account settings, Overview, Project list and the process they use" style="border: 1px solid #C3C3C3;" /> 

## Inherited versus custom objects 

Each process you create inherits the WITs provided with the parent system process&mdash;[Agile](../../work/work-items/guidance/agile-process.md), [Scrum](../../work/work-items/guidance/scrum-process.md), or [CMMI](../../work/work-items/guidance/cmmi-process.md). For example, the Agile process provides bug, task, user story, feature, epic, issue and test-related WITs. 

You can add fields and modify the workflow and form for all inherited WITs that display on the Work Item Types page. If you don't want users to use a WIT, you can disable it. In addition, you can add custom WITs. 

## Field customizations 

Locked and inherited fields correspond to fields inherited from a system process. You can't customize locked fields. You can customize some options for inherited fields. 

> [!div class="mx-tdBreakAll"]  
> |![Inherited field](_img/process/inherited-icon.png) Inherited fields |Custom fields |&nbsp;&nbsp;&nbsp;| 
> |-------------|----------|---------| 
> |- [Change the field label](customize-process-field.md#rename-field)<br/>- [Show/Hide field on form](customize-process-field.md#show-hide-field) |- [Add a custom field](customize-process-field.md#add-field)<br/>- [Add pick list (drop-down menu)](customize-process-field.md#pick-list)<br/>- [Add person-name/Identity](customize-process-field.md#identity)<br/>- [Add a rich-text (HTML) field](customize-process-field.md#html) <br/>- [Add a checkbox (Boolean) field](customize-process-field.md#boolean-field)<br/>- [Add a custom control](custom-controls-process.md) | - [Add custom rules to a field](custom-rules.md)<br/>- [Change the field label](customize-process-field.md#rename-field)<br/>- [Set Required/Default options](customize-process-field.md#options)<br/>- [Move the field within the layout](customize-process-form.md#move-field)<br/>- [Remove field from form](customize-process-field.md#remove-field)<br/>- [Delete field](customize-process-field.md#delete-field) | 

When adding custom fields, note the following limits:  
*   A maximum of 64 fields can be defined for each WIT  
*   A maximum of 512 fields can be defined per process   

In addition, you can [add an existing inherited or custom field](customize-process-field.md#add-existing-field) to another WIT within the process. For example, you can add Due Date to the user story or bug WITs.    

**What you can't customize**
- You can't change the field name or data type once you've defined it  
- With regards to pick lists, you currently can't perform these operations:
	- Change the pick list of an inherited field, such as the Activity or Discipline field  
	- Change the pick list order, pick lists display in alphabetic order
- Import or define a global list  

> [!NOTE]    
> With the Inheritance process model, you can't modify the pick-lists of pre-defined fields&mdash;such as [Activity](../../work/track/query-numeric.md), [Automation Status](../../work/track/build-test-integration.md), [Discipline](../../work/track/query-numeric.md), [Priority](../../work/track/planning-ranking-priorities.md), plus others.  

[!INCLUDE [temp](../_shared/field-reference.md)] 

[!INCLUDE [temp](../_shared/fields-become-invalid-after-customizations.md)] 

## WIT customizations 

Here are your customization options for inherited and custom WITs. 

> [!div class="mx-tdBreakAll"]  
> |![Inherited field](_img/process/inherited-icon.png) Inherited WITs | Custom WITs |&nbsp;&nbsp;&nbsp;| 
> |-------------|----------|---------| 
> |- [Add/remove custom fields](customize-process-field.md)<br/>- [Add/remove custom groups](customize-process-form.md#groups)<br/>- [Add/delete custom pages](customize-process-form.md#pages)<br/>- [Add/remove a custom control](custom-controls-process.md) <br/>- [Enable/disable](customize-process-wit.md#enable-disable) |- [Add custom WIT](customize-process-wit.md#add-wit)<br/>- [Change color or description](customize-process-wit.md#overview)<br/>- [Add/remove custom fields](customize-process-field.md)<br/>- [Add/remove custom groups](customize-process-form.md#groups)<br/>- [Add/delete custom pages](customize-process-form.md#pages)<br/>- [Add/remove a custom control](custom-controls-process.md) |- [Add, edit, or remove a workflow state](customize-process-workflow.md#states)<br/>- [Enable/disable](customize-process-wit.md#enable-disable)<br/>- [Delete](customize-process-wit.md#destroy) |  

**What you can't customize**  
- You can't add or remove an inherited WIT to or from a backlog  
- You can't change the position of an inherited field within the form layout
- You can't remove the inherited portfolio level from the product (but you can rename them)
- You can't change the name of a custom WIT. 

> [!TIP]    
> You can't calculate or set formulas using a rule. However, you may find a solution that fits your needs via the [TFS Aggregrator  (Web Service) Marketplace extension](https://marketplace.visualstudio.com/items?itemName=tfsaggregatorteam.tfs-aggregator-web-service). 
 

### Web form layout customizations 

The customizations you make to the web form only impact the work item forms displayed in a web browser. The work item forms displayed in Visual Studio or other [supported clients](../../user-guide/tools.md) won't reflect any process customizations you make.   

> [!div class="mx-tdBreakAll"]  
> |![Inherited field](_img/process/inherited-icon.png) Inherited groups |Custom groups |&nbsp;&nbsp;&nbsp;| 
> |-------------|----------|---------| 
> |- [Relabel](customize-process-form.md#groups)<br/>- [Add/remove custom fields](customize-process-field.md)<br/>- [Show/hide fields](customize-process-field.md#remove-field)<br/>![Inherited field](_img/process/inherited-icon.png) **Inherited pages**<br/>- [Relabel](customize-process-form.md#pages)<br/>- [Add/remove custom fields](customize-process-field.md)<br/>- [Add/remove a custom group](customize-process-form.md#groups) |- [Add, modify, re-sequence, delete](customize-process-form.md#groups)<br/>- [Add/remove custom fields](customize-process-field.md)<br/>- [Add/Hide a group extension](custom-controls-process.md)<br/>**Custom pages**<br/> - [Add, modify, re-sequence, delete](customize-process-form.md#pages)<br/>- [Add/delete custom fields](customize-process-field.md)<br/>- [Add/Hide a page extension](custom-controls-process.md) |    


### Workflow customizations

You customize the workflow for a WIT by adding a custom state. Each customizable WIT consists of three or more inherited states. Inherited states differ based on the system process &mdash;[Agile](../../work/work-items/guidance/agile-process.md), [Scrum](../../work/work-items/guidance/scrum-process.md), or [CMMI](../../work/work-items/guidance/cmmi-process.md)&mdash;you chose from which to create your custom process. 

> [!NOTE]    
> Before adding a workflow state, review [Workflow states and state categories](../../work/customize/workflow-and-state-categories.md) to learn how workflow states map to state categories. 

> [!div class="mx-tdBreakAll"]  
> |![Inherited field](_img/process/inherited-icon.png) Inherited states |Custom states |
> |-------------|----------|
> |- [View workflow states](customize-process-workflow.md#hide-state)<br/>- [Hide a state](customize-process-workflow.md#hide-state) |- [Add a state](customize-process-workflow.md#add-states)<br/>- [Edit a state (change color or category)](customize-process-workflow.md#edit-state)<br/>- [Remove a state](customize-process-workflow.md#remove-state) |  

**What you can't customize**  
- You can't modify an inherited state (you can't change its name, color, or category)
- You can't hide an inherited state if it's the only one in its state category    
- You can't change the name of a custom state 
- You can't add a custom state to the Completed category
- You can't change the order of states (states are listed in the order you add them within the States page, and they're listed  alphabetically within the drop down list of a work item form)  
- You can't apply a field rule to a state (for example, make a field required)
- You can't specify a Reason for a state, instead, default reasons are defined such as Moved to state Triaged, Moved out of state Triaged 
- You can't specify allowed transitions, all transitions are defined from any state to another state (except to the Removed state).  


## Backlog and board customizations 

Backlogs and boards are essential Agile tools for creating and managing work for a team. Inherited backlogs aren't locked.  

You can customize the backlogs and boards for an inherited process in the following ways. 


> [!div class="mx-tdBreakAll"]  
> |![Inherited field](_img/process/inherited-icon.png) Inherited backlogs |Custom backlogs |
> |-------------|----------|
> |- [Add a custom WIT](customize-process-backlogs-boards.md)<br/>- [Change the default WIT](customize-process-backlogs-boards.md)<br/>- [Rename the requirement backlog](customize-process-backlogs-boards.md#edit-product-backlog)<br/>- [Rename a portfolio backlog](customize-process-backlogs-boards.md#edit-portfolio-backlog) |- [Add a portfolio backlog which displays custom WITs](customize-process-backlogs-boards.md#portfolio-backlogs)<br/>- [Edit or rename a portfolio backlog](customize-process-backlogs-boards.md#edit-portfolio-backlog)<br/>- [Delete the top-level custom portfolio backlog](customize-process-backlogs-boards.md#edit-portfolio-backlog) |


When you change the default WIT for a backlog level, it causes that WIT to appear by default in the quick add panel. For example, *Customer Ticket* appears by default in the following quick add panel for the product backlog. 

<img src="_img/process/process-backlog-boards-quick-add-panel.png" alt="Product backlog, Quick Add Panel, Displays Default WIT for a backlog level" style="border: 1px solid #C3C3C3;" /> 


**What you can't customize**  
- You can't add or remove an inherited WIT to or from a backlog   
- You can't remove an inherited portfolio level from the product (but you can rename them)
- You can't insert a backlog level within the existing set of defined backlogs
- You can't reorder the backlog levels  
- You can't create a custom task level, although you can add custom WITs to the iteration backlog  
- You can't add the *Bug* work item type to any backlog level. Instead, the system allows each team to decide how they want to manage bugs. To learn more, see [Show bugs on backlogs and boards](../../work/customize/show-bugs-on-backlog.md).


 


> [!div class="mx-tdBreakAll"]  
> |![Inherited field](_img/process/inherited-icon.png) Inherited fields |Custom fields |&nbsp;&nbsp;&nbsp;| 
> |-------------|----------|---------| 
> |- [Change the field label](customize-process-field.md#rename-field)<br/>- [Show/Hide field on form](customize-process-field.md#show-hide-field) |- [Add a custom field](customize-process-field.md#add-field)<br/>- [Add pick list (drop-down menu)](customize-process-field.md#pick-list)<br/>- [Add person-name/Identity](customize-process-field.md#identity)<br/>- [Add a rich-text (HTML) field](customize-process-field.md#html) <br/>- [Add a checkbox (Boolean) field](customize-process-field.md#boolean-field)<br/>- [Add a custom control](custom-controls-process.md) |- [Add custom rules to a field](custom-rules.md)<br/>- [Change the field label](customize-process-field.md#rename-field)<br/>- [Set Required/Default options](customize-process-field.md#options)<br/>- [Move the field within the layout](customize-process-form.md#move-field)<br/>- [Remove field from form](customize-process-field.md#remove-field)<br/>- [Delete field](customize-process-field.md#delete-field) | 



  


 





## Object imits

For a list of limits placed on the number of fields, work item types, backlog levels, and other objects you can customize, see [Work tracking object limits](object-limits.md). 


<!---




<a id="return-process-overview">  </a>
## Return to the process list  
To return to the Process page, simply click the Process hub or the **All processes** breadcrumb link.   

<img src="_img/process/cprocess-open-all-processes.png" alt="Return to process overview page" style="border: 1px solid #C3C3C3;" />  

To return to a specific process and choose another WIT to customize, click the process name from the breadcrumb link.  


You can perform the following tasks with the Inheritance process model. 

> [!div class="mx-tdCol2BreakAll"]  
> |Fields  |Pick lists   |   Work item types |
> |-------------|----------|---------|
> |- [Add a custom field](customize-process-field.md)<br/>- [Add a person-name or Identity field](customize-process-field.md#identity)<br/>- [Add a rich-text field](customize-process-field.md#html)<br/>- [Add a checkbox (Boolean) field](customize-process-field.md#boolean-field)<br/>- [Add rules to a field](custom-rules.md)<br/>- [Change a field label](customize-process-field.md)<br/>- [Remove a field from a form](customize-process-field.md)<br/>- [Add a custom control field](custom-controls-process.md)<br/>- [Delete a field](customize-process-field.md#delete-field)<br/>- [Review fields](customize-process-field.md#review-fields)|- [Area paths](../set-area-paths.md)<br/>- [iteration paths](../set-iteration-paths-sprints.md)<br/>- [Person-name field (add team members)](../../accounts/add-team-members-vs.md)<br/>- [State or Reason fields](customize-process-workflow.md)<br/>- [Add a custom pick list](customize-process-form.md)|- [Add a custom field](customize-process-field.md)<br/>- [Add a custom WIT](customize-process-wit.md)<br/>- [Specify the WIT color](customize-process-wit.md)<br/>- [Customize the workflow (States)](customize-process-workflow.md)<br/>- [Customize the WIT form](customize-process-form.md)<br/>- [Add a custom control](custom-controls-process.md)| 

Choose your inherited process, the work item type and then add and edit fields from the **Layout** page. Customizations are subject to the guidelines and limitations outlined under [What is a field?](customize-process-field.md#field-reference).

> [!div class="mx-tdBreakAll"]  
> |![Inherited field](_img/process/inherited-icon.png) Inherited fields |Custom fields |&nbsp;&nbsp;&nbsp;| 
> |-------------|----------|---------| 
> |- [Change the field label](customize-process-field.md#rename-field)<br/>- [Show/Hide field on form](customize-process-field.md#show-hide-field) |- [Add a custom field](customize-process-field.md#add-field)<br/>- [Add pick list (drop-down menu)](customize-process-field.md#pick-list)<br/>- [Add person-name/Identity](customize-process-field.md#identity)<br/>- [Add a rich-text (HTML) field](customize-process-field.md#html) <br/>- [Add a checkbox (Boolean) field](customize-process-field.md#boolean-field)<br/>- [Add a custom control](custom-controls-process.md) |- [Add custom rules to a field](custom-rules.md)<br/>- [Change the field label](customize-process-field.md#rename-field)<br/>- [Set Required/Default options](customize-process-field.md#options)<br/>- [Move the field within the layout](customize-process-form.md#move-field)<br/>- [Remove field from form](customize-process-field.md#remove-field)<br/>- [Delete field](customize-process-field.md#delete-field) | 



## What you can customize

You can customize the elements listed below.To perform any of these actions, you must be a member of the Project Collection Administrators group or be [granted explicit permissions to edit a specific process](../../security/set-permissions-access-work-tracking.md#process-permissions).  
-->