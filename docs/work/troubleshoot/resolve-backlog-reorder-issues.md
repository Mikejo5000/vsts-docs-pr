---
title: Resolve backlog issues | Team Services & TFS
description: Resolve error messages when working in backlogs or boards in Visual Studio Team Services (VSTS) and Team Foundation Server (TFS)  
ms.technology: vs-devops-agile-wit
ms.prod: vs-devops-alm
ms.assetid: BDEAA5D4-83A3-49FC-BEEB-EE685E92B68B
ms.manager: douge
ms.author: kaelli
ms.topic: troubleshoot   
ms.date: 06/01/2017
---



<a id="display-hierarchy">  </a>
# Fix "Ordering backlog items is disabled" 

When a sprint backlog contains same-category, nested  work items&mdash;as described in the next section, [How backlogs and boards display hierarchical (nested) items](../backlogs-boards-plans.md#nested)&mdash;the system disables the drag-and-drop reorder feature. It does this as it determines that not all items display under these circumstances.  

To fix this, take the following actions: 

1. Click the **Create query** link on the backlog page. 
    
	![Create query of backlog](_img/backlogs-boards-create-query.png)

2. Open the query (click the link that appears). 

3. Review the list of items to determine which items are nested. For example, the following query shows that a bug is a child of a user story. Because the team has configured their backlog to display user stories and bugs at the same level (Requirements category), this corresponds to a nested item that disables the ordering feature. 

	![Query of backlog with a nested item](_img/backlogs-boards-query-nested-items.png)

4. Remove all parent-child links that exist among nested items. 

5. Return to the backlog page and refresh the page. 

## Related notes

- [Backlogs, boards, and plans](../backlogs-boards-plans.md) 