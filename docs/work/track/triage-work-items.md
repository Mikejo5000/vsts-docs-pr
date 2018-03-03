---
title: Triage work items using a work item query 
titleSuffix: VSTS & TFS  
ms.custom: Triage work items
description: Review and update work items using the triage mode from the query results view in Visual Studio Team Services and Team Foundation Server
ms.prod: vs-devops-alm
ms.technology: vs-devops-wit
ms.assetid: 486A876F-A04F-4DC7-829C-94E88BB9B7E1 
ms.topic: get-started-article
ms.manager: douge
ms.author: kaelli
ms.date: 03/01/2018
---


# Triage work items  

[!INCLUDE [temp](../_shared/version-vsts-tfs-all-versions.md)]

Using a work item query you can quickly review and update work items. Oftentimes team use the triage mode for a query to perform the following tasks: 
- Set the priority of a bug or work item 
- Assign a work item to a sprint or team member 
- Add details to the description, acceptance criteria, or repo steps 
- Link related work items 
- Update the status of work items 

In this topic you'll learn how to:

> [!div class="checklist"]
> * Use triage query mode to update a list of work items &nbsp;&nbsp;&nbsp;
> * Bulk save work items that you've updated &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 


## Open a query to triage a list of work items 

To view, open, or create a query, see [View, run, or email a work item query](view-run-query.md) or [Create managed queries with the query editor](using-queries.md). 

From the query **Results** page, you can quickly move up and down within the list of work items using the up and down arrows. As you review each work item, you can assign it, add details, set priority, or modify any field within the work item form.  

::: moniker range="vsts"

# [New Queries Experience](#tab/new-query-exp)
<!---### VSTS: New queries experience-->

To enable the New Queries Experience, see [Preview features](../../collaborate/preview-features.md). To learn more about the new experience, see [New Queries experience](queries-preview.md).  

The buttons to move up or down within the query results list are outside the work item form. Click Bottom to cycle through the choices for where the work item form appears: Bottom, Right, or Off. 

<img src="_img/triage-queries/triage-buttons-new-exp.png" alt="Web portal, choose Work hub, Queries" style="border: 1px solid #C3C3C3;" /> 

# [Old Queries Experience](#tab/new-query-exp)
<!---### VSTS: Old queries experience, TFS 2017, TFS 2015, TFS 2013-->

The buttons to move up or down within the query results list are inside the work item form. Click Bottom to cycle through the choices for where the work item form appears: Bottom, Right, or Off.

<img src="_img/triage-queries/scrum-active-bug-triage-mode-co.png" alt="Triage query results" style="border: 2px solid #C3C3C3;" />

---
::: moniker-end

::: moniker range=">= tfs-2013 <= tfs-2018"
The buttons to move up or down within the query results list are inside the work item form. Click Bottom to cycle through the choices for where the work item form appears: Bottom, Right, or Off.

<img src="_img/triage-queries/scrum-active-bug-triage-mode-co.png" alt="Triage query results" style="border: 2px solid #C3C3C3;" />

::: moniker-end
 
## Save bulk changes made to work items 

You can update several work items through the triage process, and then do a bulk save when you are finished. Work items shown in bold text indicate that local changes have not yet been saved to the data store.   


::: moniker range="vsts"

# [New Queries Experience](#tab/new-query-exp)

Click **Save items** to save all work items you've modified. 

<img src="_img/triage-queries/save-work-items-new-exp.png" alt="Choose Save work items to save all modified work items" style="border: 1px solid #C3C3C3;" /> 

# [Old Queries Experience](#tab/new-query-exp)
Click the ![double-save-icon](../_img/icons/icon-double-save.png) double-save icon to save all work items you've modified.

<img src="../backlogs/_img/bulk-modify-save-ts.png" alt="VSTS and TFS 2017, Query results page, save bulk modified items" style="border: 2px solid #C3C3C3;" />

---
::: moniker-end

::: moniker range=">= tfs-2017 <= tfs-2018"

Click the ![double-save-icon](../_img/icons/icon-double-save.png) double-save icon to save all work items you've modified.

<img src="../backlogs/_img/bulk-modify-save-ts.png" alt="VSTS and TFS 2017, Query results page, save bulk modified items" style="border: 2px solid #C3C3C3;" />

::: moniker-end

::: moniker range=">= tfs-2013 <= tfs-2015"

Click the ![double-save-icon](../_img/icons/icon-double-save.png) double-save icon to save all work items you've modified.

![TFS 2015, web portal, query results page, Bulk modify save results](../backlogs/_img/IC677240.png)  

::: moniker-end

## Related notes

- [Manage bugs](../backlogs/manage-bugs.md) 
- [Create a query](using-queries.md) 
