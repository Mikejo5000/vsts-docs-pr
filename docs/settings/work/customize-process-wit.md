---
title: Customize a work item type for an inherited process
titleSuffix: Codex Agile
description: Customize a process by adding or modifying a work item type for a Codex project 
ms.technology: devops-agile
ms.prod: devops
ms.assetid: DBF41880-62A4-43A9-9A31-8DB701EB888E
ms.manager: douge
ms.author: kaelliauthor: KathrynEE
monikerRange: 'vsts'
ms.topic: conceptual
ms.date: 03/20/2018
---

# Add and manage work item types      

[!INCLUDE [temp](../../_shared/codex-agile.md)]

You use different work item types (WITs) to plan and track different types of work. Your Codex project contains 9 or more WITs that you can customize, based on the process&mdash;[Agile](../../work/work-items/guidance/agile-process.md), [Scrum](../../work/work-items/guidance/scrum-process.md), or [CMMI](../../work/work-items/guidance/cmmi-process.md)&mdash;used to create your  project. Also, you can add a custom WIT to support additional tracking requirements. 

For example, you may want to capture customer issues in a custom Ticket WIT.   

<img src="_img/process/custom-wit-new-ticket-form.png" alt="Custom Ticket work item form" style="border: 1px solid #C3C3C3;" /> 

[!INCLUDE [temp](../_shared/process-prerequisites.md)] 

[!INCLUDE [temp](../_shared/open-process-admin-context-ts.md)]
 
[!INCLUDE [temp](../_shared/automatic-update-project.md)] 

<a id="add-wit">  </a>
## Add a work item type

0. From the Work Item Types page, click ![green plus icon](../../_img/icons/green-plus-new-field-icon.png) New work item type.

	<img src="_img/process/cpwit-add-new-wit.png" alt="Process hub, Inherited process, Work Item Types, Add new work item type" style="border: 2px solid #C3C3C3;" />
 
0. Name the WIT and optionally specify a description, icon and color. The icon and color you specify will appear throughout the web portal, including on the work item form and when associated work items appear on a backlog, boards, query results, and more. Click Create to save. 

	<img src="_img/process/cwit-create-wit-ticket.png" alt="Create new work item type dialog" style="border: 1px solid #C3C3C3;" /> 

	Each new WIT comes predefined with a Details page with the Description field, and Discussion, Development, and Related Work groups. Also added, but not shown nor editable, are the standard elements included with the header of the form as shown in the following image, as well as the history, links, and attachment pages. 
 
	<img src="_img/process/weblayout-system-controls-details-page.png" alt="WIT header details" style="border: 1px solid #C3C3C3;" /> 

0.   From the Layout page, you can add fields, groups, or pages to specify the form and fields you want to track. For details, see [Customize a field](customize-process-field.md) or [Customize a web form for a process](customize-process-form.md).    

	<img src="_img/process/cpwit-new-ticket-define.png" alt="New WIT, customize layout" style="border: 1px solid #C3C3C3;" /> 	

0. Open the States page to view the default workflow states. Optionally, [customize the workflow states](customize-process-workflow.md).  
<a id="backlog">  </a> 

0. Optional. To add the WIT to a backlog, see [Customize your backlogs or boards for a process](customize-process-backlogs-boards.md). By default, custom WITs aren't added to any backlog. To learn more about different backlog levels, see [Backlogs, boards, and plans](../../work/backlogs-boards-plans.md).   

0. Verify the custom work item type appears as expected. Either navigate to the backlog or board to which you added the custom WIT, or open the Work hub menu and open a new work item of the type you added.  

	<img src="_img/process/cpwit-new-custom-work-item-ticket.png" alt="stories Kanban board, add new custom ticket work item" style="border: 1px solid #C3C3C3;" /> 

	If you don't see the custom WIT, refresh your browser to make sure it registers all the custom changes you've made. 

<a id="overview">  </a>
## Change description, icon or color of a custom WIT 

To change the description, icon or color of a custom WIT, choose Edit from the WIT context menu. 

Here we change the description, icon and color for the Ticket custom WIT.  

<img src="_img/process/cpwit-edit-color-description.png" alt="Overview page, edit custom ticket description, icon and color" style="border: 1px solid #C3C3C3;" /> 

<a id="enable-disable"></a>
## Enable or disable a custom WIT  

You can disable a custom WIT which will prevent users from being able to add new work items using it. However, all existing work items defined using the custom WIT remain in the data store.  

You may want to disable a custom WIT until you have defined all the fields, workflow, and form layout that you have planned.

To disable a custom WIT, choose Disable from the WIT context menu. 

To re-enable the WIT, choose Enable from the WIT context menu. 

> [!NOTE]    
>Disabling a WIT will remove the work item type from the New drop down and add experiences. Creating a work item of that WIT will also be blocked via REST APIs.  
>
>No changes are made to existing work items of that type. You can update or delete them and they will continue to appear on backlogs and boards. Also, you can change the work item type of disabled WITs to an enabled type, but you can't change the type to a disabled WIT.


## Related articles  

As you customize a WIT, all projects that reference the inherited process that you're customizing will automatically update to reflect the custom WITs you've added. To view your customizations, refresh your web browser.  

To customize a single project, always start by [creating an inherited process and migrating the project to that process](manage-process.md). Then, all the customizations that you make to the inherited process automatically appear for the project you migrated.  

See also:  

- [Customize a field](customize-process-field.md)  
- [Customize a form](customize-process-field.md)
- [Customize a workflow for a work item type](customize-process-field.md)
- [Customize a process](customize-process-field.md) 

<a id="destroy">  </a>
### Delete or destroy a custom WIT 

> [!IMPORTANT]  
> Destroying a WIT will delete all work items and data associated with that WIT, including historical values. Once destroyed, you can't recover the data. 

1. To completely remove a custom WIT and all work items based on that WIT, click the Destroy option from the WIT context menu.

	To destroy a WIT, you must be a member of the Project Collection Administrators group or be [granted explicit permissions to edit a specific process](../../security/set-permissions-access-work-tracking.md#process-permissions). 

2. To complete the delete operation, you must type the name of the WIT as shown. 

	<img src="_img/process/cpit-destroy-wit-confirm.png" alt="Delete field, confirmation dialog" style="border: 1px solid #C3C3C3;" />  
 

<!---
### WIT extensibility

Using REST APIs you can add .... 

-->




