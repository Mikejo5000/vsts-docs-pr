---
title: Inheritance process model
titleSuffix: VSTS
description: Guide to configuring and customizing work tracking features in Visual Studio Team Services

title: What is an inherited process?  
titleSuffix: Codex Agile
description: Describes what an inherited process is and how you use it to customize the work tracking system and Agile tools for a Codex Agile project 

ms.technology: devops-agile
ms.prod: devops
ms.assetid: 
ms.manager: douge
ms.author: kaelliauthor: KathrynEE
monikerRange: 'vsts'
ms.date: 03/20/2018
---




# Inheritance process model  

[!INCLUDE [temp](../../_shared/codex-agile.md)]

<a id="inheritance"> </a> 

The Inheritance process model provides support for customizing work tracking objects and Agile tools for a team project through the user interface. Team projects inherit the customizations made to a process.


You can perform the following tasks with the Inheritance process model. 

> [!div class="mx-tdCol2BreakAll"]  
> |Fields  |Pick lists   |   Work item types |
> |-------------|----------|---------|
> |- [Add a custom field](customize-process-field.md)<br/>- [Add a person-name or Identity field](customize-process-field.md#identity)<br/>- [Add a rich-text field](customize-process-field.md#html)<br/>- [Add a checkbox (Boolean) field](customize-process-field.md#boolean-field)<br/>- [Add rules to a field](custom-rules.md)<br/>- [Change a field label](customize-process-field.md)<br/>- [Remove a field from a form](customize-process-field.md)<br/>- [Add a custom control field](custom-controls-process.md)<br/>- [Delete a field](customize-process-field.md#delete-field)<br/>- [Review fields](customize-process-field.md#review-fields)|- [Area paths](set-area-paths.md)<br/>- [iteration paths](set-iteration-paths-sprints.md)<br/>- [Person-name field (add team members)](../../accounts/add-team-members-vs.md)<br/>- [State or Reason fields](customize-process-workflow.md)<br/>- [Add a custom pick list](customize-process-form.md)|- [Add a custom field](customize-process-field.md)<br/>- [Add a custom WIT](customize-process-wit.md)<br/>- [Specify the WIT color](customize-process-wit.md)<br/>- [Customize the workflow (States)](customize-process-workflow.md)<br/>- [Customize the WIT form](customize-process-form.md)<br/>- [Add a custom control](custom-controls-process.md)| 


> [!div class="mx-tdCol2BreakAll"]  
> | Backlogs | Process |  
> |----------|---------|   
> |- [Add custom backlog levels](../../work/customize/add-portfolio-backlogs.md)<br/>- [Add a custom WIT to a backlog](customize-process-backlogs-boards.md)<br/>- [Show bugs on backlogs/boards](../../work/customize/show-bugs-on-backlog.md)|- [Create & manage an inherited process](manage-process.md)<br/>- [Customize a process](customize-process.md) |


 
> [!NOTE]    
> With the Inheritance process model, you can't modify the pick-lists of pre-defined fields&mdash;such as [Activity](../track/query-numeric.md), [Automation Status](../track/build-test-integration.md), [Discipline](../track/query-numeric.md), [Priority](../track/planning-ranking-priorities.md), plus others.  


Use this sequence to create and apply an inherited process to a Codex project. 

[![Create an inherited process](_img/process/customize-work-phase2-step1.png)](manage-process.md#create-inherited-process)[![Customize the inherited process](_img/process/customize-work-phase2-step2.png)](customize-process.md)[![Apply inherited process to team project(s)](_img/process/customize-work-phase2-step3.png)](manage-process.md#migrate)![Refresh and verify changes](_img/process/customize-work-phase2-step4.png)  


