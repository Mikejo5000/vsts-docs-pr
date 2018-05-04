---
title: About process customization and  inherited processes 
titleSuffix: Codex Agile
description: Describes what an inherited process is and how you use it to customize the work tracking system and Agile tools for a Codex Agile project 
ms.technology: devops-agile
ms.prod: devops
ms.assetid: 
ms.manager: douge
ms.author: kaelliauthor: KathrynEE
ms.topic: conceptual 
monikerRange: 'vsts'
ms.date: 03/20/2018
---




# About process customization and  inherited processes  

[!INCLUDE [temp](../../_shared/codex-agile.md)]

<a id=" inherited "> </a> 

The Inheritance process model provides support for customizing work tracking objects and Agile tools for a team project through the user interface. Team projects inherit the customizations made to a process.


You can perform the following tasks with the Inheritance process model. 

> [!div class="mx-tdCol2BreakAll"]  
> |Fields  |Pick lists   |   Work item types |
> |-------------|----------|---------|
> |- [Add a custom field](customize-process-field.md)<br/>- [Add a person-name or Identity field](customize-process-field.md#identity)<br/>- [Add a rich-text field](customize-process-field.md#html)<br/>- [Add a checkbox (Boolean) field](customize-process-field.md#boolean-field)<br/>- [Add rules to a field](custom-rules.md)<br/>- [Change a field label](customize-process-field.md)<br/>- [Remove a field from a form](customize-process-field.md)<br/>- [Add a custom control field](custom-controls-process.md)<br/>- [Delete a field](customize-process-field.md#delete-field)<br/>- [Review fields](customize-process-field.md#review-fields)|- [Area paths](../set-area-paths.md)<br/>- [iteration paths](../set-iteration-paths-sprints.md)<br/>- [Person-name field (add team members)](../../accounts/add-team-members-vs.md)<br/>- [State or Reason fields](customize-process-workflow.md)<br/>- [Add a custom pick list](customize-process-form.md)|- [Add a custom field](customize-process-field.md)<br/>- [Add a custom WIT](customize-process-wit.md)<br/>- [Specify the WIT color](customize-process-wit.md)<br/>- [Customize the workflow (States)](customize-process-workflow.md)<br/>- [Customize the WIT form](customize-process-form.md)<br/>- [Add a custom control](custom-controls-process.md)| 


> [!div class="mx-tdCol2BreakAll"]  
> | Backlogs | Process |  
> |----------|---------|   
> |- [Add custom backlog levels](../../work/customize/add-portfolio-backlogs.md)<br/>- [Add a custom WIT to a backlog](customize-process-backlogs-boards.md)<br/>- [Show bugs on backlogs/boards](../../work/customize/show-bugs-on-backlog.md)|- [Create & manage an inherited process](manage-process.md)<br/>- [Customize a process](customize-process.md) |


 
> [!NOTE]    
> With the Inheritance process model, you can't modify the pick-lists of pre-defined fields&mdash;such as [Activity](../../work/track/query-numeric.md), [Automation Status](../../work/track/build-test-integration.md), [Discipline](../../work/track/query-numeric.md), [Priority](../../work/track/planning-ranking-priorities.md), plus others.  


> [!div class="mx-tdBreakAll"]  
> |![Inherited field](_img/process/inherited-icon.png) Inherited fields |Custom fields |&nbsp;&nbsp;&nbsp;| 
> |-------------|----------|---------| 
> |- [Change the field label](customize-process-field.md#rename-field)<br/>- [Show/Hide field on form](customize-process-field.md#show-hide-field) |- [Add a custom field](customize-process-field.md#add-field)<br/>- [Add pick list (drop-down menu)](customize-process-field.md#pick-list)<br/>- [Add person-name/Identity](customize-process-field.md#identity)<br/>- [Add a rich-text (HTML) field](customize-process-field.md#html) <br/>- [Add a checkbox (Boolean) field](customize-process-field.md#boolean-field)<br/>- [Add a custom control](custom-controls-process.md) |- [Add custom rules to a field](custom-rules.md)<br/>- [Change the field label](customize-process-field.md#rename-field)<br/>- [Set Required/Default options](customize-process-field.md#options)<br/>- [Move the field within the layout](customize-process-form.md#move-field)<br/>- [Remove field from form](customize-process-field.md#remove-field)<br/>- [Delete field](customize-process-field.md#delete-field) | 


<a id="what-you-can-customize">  </a>
## What you can customize

You can customize the elements listed below. Some options of inherited elements are locked and can't be customized. To perform any of these actions, you must be a member of the Project Collection Administrators group or be [granted explicit permissions to edit a specific process](../../security/set-permissions-access-work-tracking.md#process-permissions).  

> [!NOTE]    
>For a list of limits placed on the number of fields, work item types, backlog levels, and other objects you can customize, see [Work tracking object limits](object-limits.md). 


### Fields

Choose your inherited process, the work item type and then add and edit fields from the **Layout** page. Customizations are subject to the guidelines and limitations outlined under [What is a field?](customize-process-field.md#field-reference).

> [!div class="mx-tdBreakAll"]  
> |![Inherited field](_img/process/inherited-icon.png) Inherited fields |Custom fields |&nbsp;&nbsp;&nbsp;| 
> |-------------|----------|---------| 
> |- [Change the field label](customize-process-field.md#rename-field)<br/>- [Show/Hide field on form](customize-process-field.md#show-hide-field) |- [Add a custom field](customize-process-field.md#add-field)<br/>- [Add pick list (drop-down menu)](customize-process-field.md#pick-list)<br/>- [Add person-name/Identity](customize-process-field.md#identity)<br/>- [Add a rich-text (HTML) field](customize-process-field.md#html) <br/>- [Add a checkbox (Boolean) field](customize-process-field.md#boolean-field)<br/>- [Add a custom control](custom-controls-process.md) |- [Add custom rules to a field](custom-rules.md)<br/>- [Change the field label](customize-process-field.md#rename-field)<br/>- [Set Required/Default options](customize-process-field.md#options)<br/>- [Move the field within the layout](customize-process-form.md#move-field)<br/>- [Remove field from form](customize-process-field.md#remove-field)<br/>- [Delete field](customize-process-field.md#delete-field) | 



> [!NOTE]  
> When you change a project to use an inherited process, you may find one or more Agile tools or work items appear in an invalid state. For example: 
> 
> - If you make a field required, work items with that field undefined will show an error message. You'll need to resolve the errors to make additional changes and save the work item. 
> - If you add or remove/hide workflow states of a WIT that appears on the Kanban board, you'll need to update the Kanban board column configurations for all teams defined in the team project. 




### Work item types

Choose your inherited process, and then add or edit a work item type from the **Work item types** page.

> [!div class="mx-tdBreakAll"]  
> |![Inherited field](_img/process/inherited-icon.png) Inherited WITs | Custom WITs |&nbsp;&nbsp;&nbsp;| 
> |-------------|----------|---------| 
> |- [Add/remove custom fields](customize-process-field.md)<br/>- [Add/remove custom groups](customize-process-form.md#groups)<br/>- [Add/delete custom pages](customize-process-form.md#pages)<br/>- [Add/remove a custom control](custom-controls-process.md) <br/>- [Enable/disable](customize-process-wit.md#enable-disable) |- [Add custom WIT](customize-process-wit.md#add-wit)<br/>- [Change color or description](customize-process-wit.md#overview)<br/>- [Add/remove custom fields](customize-process-field.md)<br/>- [Add/remove custom groups](customize-process-form.md#groups)<br/>- [Add/delete custom pages](customize-process-form.md#pages)<br/>- [Add/remove a custom control](custom-controls-process.md) |- [Add, edit, or remove a workflow state](customize-process-workflow.md#states)<br/>- [Enable/disable](customize-process-wit.md#enable-disable)<br/>- [Delete](customize-process-wit.md#destroy) |  



### Web form layout  

Choose your inherited process and the work item type, and then modify the form from the **Layout** page.

> [!div class="mx-tdBreakAll"]  
> |![Inherited field](_img/process/inherited-icon.png) Inherited groups |Custom groups |&nbsp;&nbsp;&nbsp;| 
> |-------------|----------|---------| 
> |- [Relabel](customize-process-form.md#groups)<br/>- [Add/remove custom fields](customize-process-field.md)<br/>- [Show/hide fields](customize-process-field.md#remove-field)<br/>![Inherited field](_img/process/inherited-icon.png) **Inherited pages**<br/>- [Relabel](customize-process-form.md#pages)<br/>- [Add/remove custom fields](customize-process-field.md)<br/>- [Add/remove a custom group](customize-process-form.md#groups) |- [Add, modify, re-sequence, delete](customize-process-form.md#groups)<br/>- [Add/remove custom fields](customize-process-field.md)<br/>- [Add/Hide a group extension](custom-controls-process.md)<br/>**Custom pages**<br/> - [Add, modify, re-sequence, delete](customize-process-form.md#pages)<br/>- [Add/delete custom fields](customize-process-field.md)<br/>- [Add/Hide a page extension](custom-controls-process.md) |    


### Workflow states

Choose your inherited process, the work item type, and then modify the workflow from the **States** page.  

> [!div class="mx-tdBreakAll"]  
> |![Inherited field](_img/process/inherited-icon.png) Inherited states |Custom states |
> |-------------|----------|
> |- [View workflow states](customize-process-workflow.md#hide-state)<br/>- [Hide a state](customize-process-workflow.md#hide-state) |- [Add a state](customize-process-workflow.md#add-states)<br/>- [Edit a state (change color or category)](customize-process-workflow.md#edit-state)<br/>- [Remove a state](customize-process-workflow.md#remove-state) |   

### Backlogs 
Choose your inherited process, and then modify the backlogs configuration from the **Backlog levels** page. Inherited backlogs aren't locked. 


> [!div class="mx-tdBreakAll"]  
> |![Inherited field](_img/process/inherited-icon.png) Inherited backlogs |Custom backlogs |
> |-------------|----------|
> |- [Add a custom WIT](customize-process-backlogs-boards.md)<br/>- [Change the default WIT](customize-process-backlogs-boards.md)<br/>- [Rename the requirement backlog](customize-process-backlogs-boards.md#edit-product-backlog)<br/>- [Rename a portfolio backlog](customize-process-backlogs-boards.md#edit-portfolio-backlog) |- [Add a portfolio backlog which displays custom WITs](customize-process-backlogs-boards.md#portfolio-backlogs)<br/>- [Edit or rename a portfolio backlog](customize-process-backlogs-boards.md#edit-portfolio-backlog)<br/>- [Delete the top-level custom portfolio backlog](customize-process-backlogs-boards.md#edit-portfolio-backlog) |

## Web versus Visual Studio form layouts 

The customizations you make only impact the work item forms displayed in a web browser. The work item forms displayed in Visual Studio or other [supported clients](../../user-guide/tools.md) won't reflect any process customizations you make.    


<a id="return-process-overview">  </a>
## Return to the process list  
To return to the Process page, simply click the Process hub or the **All processes** breadcrumb link.   

<img src="_img/process/cprocess-open-all-processes.png" alt="Return to process overview page" style="border: 1px solid #C3C3C3;" />  

To return to a specific process and choose another WIT to customize, click the process name from the breadcrumb link.  


[!INCLUDE [temp](../../work/_shared/field-reference.md)] 
