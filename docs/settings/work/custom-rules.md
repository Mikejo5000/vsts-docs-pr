---
title: Add a custom rule to a work item type to an inherited process
titleSuffix: Codex Agile
description: Add a custom rule to a work item type defined for an  inherited process and Codex project
ms.technology: devops-agile
ms.prod: devops
ms.assetid: 17A6AF2C-81E9-4717-971E-2621613AEB31  
ms.manager: douge
ms.author: kaelliauthor: KathrynEE
monikerRange: 'vsts'
ms.topic: conceptual
ms.date: 03/23/2018
---


# Add a rule to a work item type  

[!INCLUDE [temp](../../_shared/codex-agile.md)]

Custom rules provide support for a number of business use cases, allowing you to go beyond setting a default value for a field or make it required. Rules allow you to clear the value of a field, copy a value into a field, and apply values based on dependencies between different fields' values. 

With a custom rule, you can define a number of actions based on one or two conditions. For example, you can apply a rule to support these types of scenarios: 

- When a value is defined for Priority, then make Risk a required field 
- When a change is made to the value of Release, then clear the value of "Milestone"     
- When a change was made to the value of Remaining Work, then make Completed Work a required field
- When the value of Approved is True, then make Approved By a required field 
- When a user story is created, make make the following fields required: Priority, Risk, and  Effort

> [!TIP]    
> You can't calculate or set formulas using a rule. However, you may find a solution that fits your needs via the [TFS Aggregrator  (Web Service) Marketplace extension](https://marketplace.visualstudio.com/items?itemName=tfsaggregatorteam.tfs-aggregator-web-service). 

## Rule composition  

Each rule consists of two parts: Conditions and Actions. Conditions define the circumstances which must be met in order for the rule to be applied. Actions define the operations to perform. You can specify a maximum of two conditions and 10 actions per rule. All custom rules require all conditions to be met in order to be run. 

It's important to note that these are system-level rules, not just form-level rules. For example, setting a field as read-only will not only apply the rule on the work item form, but also through the API and Excel based Add-in. Also when applying a condition that sets or clears the value of another field, that is not written to the history of the work item. The rule is applied to the data that is being displayed (e.g. work item form, API results, Excel Add-in, etc.).
 
As an example, you can make a field required based on value assignments made to two other fields. In this case, you would specify two conditions and one action. For example: 

	(Condition) When the value of Reason = Verified Fixed  
	(Condition) And when the value of the Tech Lead = Jamal Hartnett   
	(Action) Then make the Integration Build field required   

> [!div class="mx-tdBreakAll"]  
> |Supported conditions |Supported actions  |
> |-------------|----------|  
> |- A work item state changes to a selected state<br/>- A work item state changes from one state to another state<br/>- A work item is created<br/>- A work item state is in a selected state<br/>- The value of a field equals a specified value<br/>- The value of a field does not equal a specified value<br/>- A value is defined for a field<br/>- No value is defined for a field<br/>- A change was made to the value of a field<br/>- No change was made to the value of a field |- Clear the value of a field<br/>- Copy the value of a field to another field<br/>- Make a field read-only  <br/>- Make a field required<br/>- Set the value of a field<br/>- Set the value of a field to the current date-time<br/>- Set the value of a field to the current user  |


> [!NOTE]     
>You make a field required and specify a field default through the [**Options** tab for the field](customize-process-field.md#options).  

[!INCLUDE [temp](../_shared/process-prerequisites.md)] 

[!INCLUDE [temp](../_shared/open-process-admin-context-ts.md)]
 
[!INCLUDE [temp](../_shared/automatic-update-project.md)] 

## Add a custom rule 

You add fields to a selected work item type.  
	
0. Select the WIT to which you want to add a rule, choose **Rules**, and then choose **New rule**.   

	> [!div class="mx-imgBorder"]  
	> ![Process, WIT, Bug, Layout, New custom control](_img/rules/custom-rule-create-rule.png)  

0. Name the rule and select the condition(s) and action(s) from the dropdown menus.     

	> [!TIP]  
	>Specify a name that builds off the field(s) you're acting on, or the conditions you're setting.  
	
	Here we define that the Acceptance Criteria field is required when the State changes to Active and it is currently empty. 

    <img src="_img/process/custom-rule-create-rule-form.png" alt="New rule form" style="border: 1px solid #C3C3C3;" /> 
 
	> [!NOTE]    
	>The sequence of actions you specify doesn't impact the behavior of the rule itself or its behavior with respect to other rules defined for the same WIT. 

0. Once you've added a custom rule, open a work item and verify that the rule works as you intended. 

<a id="delete-disable">  </a>
## Delete or disable a rule     

You can temporarily disable a rule or delete it altogether.  

You delete or disable the rule from the actions menu of the rule.  

<img src="_img/process/custom-rule-delete-disable-rule.png" alt="Delete or disable a rule" style="border: 1px solid #C3C3C3;" />  

<!---
<a id="system-rules">  </a>
## System rules

Each work item type&mdash;bug, task, user story, etc.&mdash;has several system rules already defined. Some are simple, like making the Title field required or setting a default for the Value Area field. In addition, a number of system rules define actions to take when a workflow state changes. 

For example, several rules exist to copy the current user identity under the following conditions: 
- When a work item is modified, copy the user identity to the Changed By field  
- When a work item is modified, copy the user identity to the Changed By field
- When the workflow state changes to Closed or Done, copy the user identity to the Closed By field. 
 
> [!IMPORTANT]  
> Predefined system rules will take precedent over any custom rule that you define which would overwrite it.  

-->

## Related articles   

- [Customize the form](customize-process-form.md)
- [Customize a process](customize-process.md)    



