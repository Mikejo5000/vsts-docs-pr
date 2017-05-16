---
title: Define features and epics | Team Services & TFS  
description:  Define features and epics to group backlog items and track high level items 
ms.technology: vs-devops-agile-wit
ms.prod: vs-devops-alm
ms.assetid: 9B517FEE-14FA-41FA-87CD-99D33168D01E  
ms.manager: douge
ms.author: kaelli
ms.topic: get-started-article  
ms.date: 05/10/2017
--- 

# Define features and epics  

**Team Services | TFS 2017 | TFS 2015 | TFS 2013**  

While many teams can work with a flat list of items, sometimes it helps to group related items into a hierarchical structure. 
Perhaps you like to start with a big picture and break it down into smaller deliverables. 
Or, you've got an existing backlog and now need to organize it.   

No matter your starting point, you can use portfolio backlogs to bring more order to your backlog. 
Use your backlogs to plan your project and to:  
*	Manage a portfolio of features that are supported by different development and management teams  
*	Group items into a release train  
*	Minimize size variability of your deliverables by breaking down a large feature into smaller backlog items     

>[!NOTE]  
>**Feature availability**: Epics are supported on Team Services and TFS 2015 and later versions. Each team can choose the backlog levels that are active as described in [Select backlog navigation levels for your team](../customize/select-backlog-navigation-levels.md).  

With portfolio backlogs you can quickly add and group items into a hierarchy, drill up or down within the hierarchy, reorder and reparent items, and filter hierarchical views. Portfolio backlogs are one of three classes of backlogs available to you. For an overview of the features supported on each backlog and the two types of boards, see [Backlogs, boards, and plans](../backlogs-boards-plans.md).  

[!INCLUDE [temp](../_shared/image-differences.md)]



<a id="view-portfolio-backlog" />
## View a backlog or portfolio backlog 
To focus on one level of a backlog at a time, click the name of the backlog you want to view. If you don't see all three backlog levels&mdash;
Epics, Features, and Backlog items&mdash;
you can [enable them for your team](../customize/select-backlog-navigation-levels.md). 

For example, when you click Epics, you'll see a list of all Epics in your team's active area paths. From there, you can drill down to see child features and backlog items.  

<img src="_img/org-backlog-epics-ts-new-nav.png" alt="Hierarchical view of backlogs" style="border: 1px solid #CCCCCC;" />  

Click Features to see a list of all features in your team's active area paths.  


<a name="add-features-epics"></a>
<a name="add-features"></a>
## Add features and epics 
Just as you can [add items to your product backlog](create-your-backlog.md), you can add items to your features and epics backlogs. 
Here, we've added six features. 

<img src="_img/org-backlog-features-ts-new-nav.png" alt="Features backlog" style="border: 1px solid #CCCCCC;" />  

You can add epics in the same way. Simply open the Epics backlog.  

Open each item (double-click, or press Enter to open the selected item) and add all the info you want to track. Enter as much detail as the team needs to understand the scope, estimate the work required, develop tests, and ensure that the end product meets acceptance criteria.

>[!NOTE]  
>**Reminder:** The following screenshots illustrate the work item form for Team Services. Your forms may differ depending on what you have enabled, what process you chose when creating your team project&mdash;[Agile](../guidance/agile-process.md), [Scrum](../guidance/scrum-process.md), or [CMMI](../guidance/cmmi-process.md)&mdash;and what platform you're working from, Team Services or TFS.  

<img src="_img/org-backlog-feature-form-ts-new-nav.png" alt="Feature work item form, Agile process, Add details to a feature" style="border: 1px solid #CCCCCC;" /> 
 
<table>
<tbody valign="top">
<tr>
<th>Field</th>
<th>Usage</th>
</tr>
<tr>
<td>
[Value Area](../track/planning-ranking-priorities.md)
</td>
<td>The area of customer value addressed by the epic, feature, or backlog item. Values include:  
<ul>
<li><b>Architectural</b> – technical services to implement business features that deliver solution </li> 
<li><b>Business</b> (Default) – services that fulfill customers or stakeholder needs that directly deliver customer value to support the business </li>
</ul>
</td>
</tr>
<tr>
<td>
[Effort](../track/query-numeric.md)
</td>
<td>
Provide a relative estimate of the amount of work required to complete a Feature or Epic. Use any numeric unit of measurement your team prefers. Some options are [story points, time, or other relative unit](create-your-backlog.md#estimates).<br />For user stories and requirements, you capture estimates in the Story Points and Size fields. These fields support usage of the [velocity and forecast](../scrum/velocity-and-forecasting.md) tools. 
</td>
</tr>

<tr>
<td>

[Business Value](../track/query-numeric.md)
</td>
<td>
Specify a priority that captures the relative value of an Epic, Feature, or backlog item compared to other items of the same type. The higher the number, the greater the business value.<br />Use this field when you want to capture a priority separate from the changeable backlog stack ranking.

</td>
</tr>

<tr>
<td>
[Time Criticality](../track/planning-ranking-priorities.md)
</td>
<td>
A subjective unit of measure that captures the how the business value decreases over time. Higher values indicate that the Epic or Feature is inherently more time critical than those items with lower values. 
</td>
</tr>
<tr>
	<td><p>[Target Date](../track/query-by-date-or-current-iteration.md)</p></td>
	<td><p>Specify the date by which the feature should be implemented.</p></td></tr>

</tbody>
</table>




## Add child items
With your features defined, you're ready to add child items to them. From any backlog, you can add child items. 
You can add features to epics, and backlog items to features. 
 
Here we add a product backlog item as a child to the Customer Web - Phase 1 feature. 

<img src="_img/org-backlog-features-add-child-ts.png" alt="Add a child item to a backlog work item" style="border: 1px solid #CCCCCC;" />  


Whenever you see the plus ![plus icon](../_img/icons/green_plus_icon.png) , you can add a child item. 
The work item always corresponds to the hierarchy of work item types that are defined for your team project.   

For Scrum team projects, your hierarchy is as shown: 

![Hierarchical view of backlogs](_img/ALM_OB_Scrum_WIT_Hier_C.png) 

Because [teams can also set bugs as tasks](../customize/show-bugs-on-backlog.md), bugs can be added as children of PBIs. 

The work item types you'll see depends on the [process you selected to create your team project](../guidance/choose-process.md). 

If you want bugs to show up on your backlog and you're not seeing them, [enable them for your team](../customize/show-bugs-on-backlog.md). 

 
## Try this next

Once you've defined features and epics, you can now [organize your backlog](organize-backlog.md) by mapping or drag-and-drop operations.  

## Related notes  

Portfolio backlogs are not only a great way to organize your project plan, but also a great way to provide visibility of project plans across enterprise teams. With portfolio backlogs, management teams can gain insight into project status across all their development teams. 

- [Backlogs, boards, and plans](../backlogs-boards-plans.md)  
- [Work with multi-team ownership of backlog items](work-multi-team-ownership-backlogs.md)  
- [Create your backlog](create-your-backlog.md)  
- [Select backlog navigation levels for your team](../customize/select-backlog-navigation-levels.md)   
- [Customize your backlogs or boards for a process](../process/customize-process-backlogs-boards.md)  
- [Add portfolio backlogs](../customize/add-portfolio-backlogs.md)  


> [!NOTE]
> To understand the features supported on each backlog and board, and how each display hierarchical items, see [Backlogs, boards, and plans](../backlogs-boards-plans.md). To learn how to track progress across teams, see [Visibility across teams](../scale/visibility-across-teams.md).    
 
A few things to keep in mind...
*   Every team owns their own backlog, to create a new backlog you [create a new team](../scale/multiple-teams.md) 
*   Every backlog has a corresponding [Kanban board](../kanban/kanban-basics.md) you can use to track progress and update status  
*   Each team can control how [bugs show up on their backlogs ](../customize/show-bugs-on-backlog.md)   
*   To have work performed by several teams roll up in to a portfolio backlog, you'll want to [setup the team hierarchy](../scale/portfolio-management.md) 
*   When you add child items they're linked to their parent using parent-child links which support hierarchical views and [tree queries](../track/using-queries.md#tree-query)    
*   If you need more than three backlog levels, you can add more based on the process model you use: 
	- **Inheritance**: [Customize your backlogs or boards for a process](../process/customize-process-backlogs-boards.md)  
	- **Hosted XML or On-premises XML**: [Add portfolio backlogs](../customize/add-portfolio-backlogs.md).  

### Backlog controls

| Control           | Function     |
|------------------|-------------|
| Backlog          | Switch to backlog view   |
| Board          | [Switch to Kanban board view](../kanban/kanban-basics.md)  |
| Forecast: On/Off     | [Turn forecast tool on/off](http://msdn.microsoft.com/Library/Work/scrum/velocity-and-forecasting.md) (appears only when Parents is set to Hide, and only available for the product backlog) |
| Mapping: On/Off     | [Turn mapping Off/On](#mapping)    |
| Parents: Show/Hide         | Turn tree hierarchy on/off     |
| In progress items: Show/Hide    |Show or hide list of backlog items whose State is active or in progress       |
| ![Settings icon](../_img/icons/team-settings-gear-icon.png)  | Configure team settings: [Backlogs](../customize/select-backlog-navigation-levels.md), [Working days](../scale/capacity-planning.md#team_settings), [Working with bugs](../customize/show-bugs-on-backlog.md)   |
| ![full screen icon](../_img/icons/fullscreen_icon.png)/![exit full screen icon](../_img/icons/exitfullscreen_icon.png)   | Enter or exit full screen mode   |
| ![expand icon](../_img/icons/expand_icon.png) / ![collapse icon](../_img/icons/collapse_icon.png)    | Expand or collapse one level of the tree hierarchy   |
| ![mail icon](../_img/icons/mail_icon.png)  | Email a copy of your backlog |
| ![Filter](../_img/icons/tag_filter_icon.png)    | [Turn tag filtering On/Off ](../track/add-tags-to-work-items.md)  |


Note that even if you have show parents turned on, the **Create query** and mail ![mail icon](../_img/icons/mail_icon.png) controls will only list items at the currently selected level. 

See also [Keyboard shortcuts](../../reference/keyboard-shortcuts.md).  

[!INCLUDE [temp](../_shared/filter-backlog-or-board.md)]

[!INCLUDE [temp](../_shared/assign-to-sprint.md)]
