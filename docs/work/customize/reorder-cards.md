---
title: Set Kanban board card reordering
titleSuffix: VSTS & TFS
description: Use the Kanban board, process, and tools to plan and track work in Visual Studio Team Services and Team Foundation Server 
ms.technology: vs-devops-wit
ms.prod: vs-devops-alm
ms.assetid: BDB9CF5A-D83C-4823-BD53-29D49F797FB4
monikerRange: vsts || >= tfs-2013 <= tfs-2018
ms.manager: douge
ms.author: kaelli
ms.date: 03/01/2018
---


# Reorder cards  
<b>VSTS | TFS 2018 | TFS 2017 | TFS 2015</b> 

::: moniker range="tfs-2013"
> [!NOTE]   
> Reordering cards is not a supported feature in TFS 2013. Consider upgrading to TFS 2015.1 or later version. 
::: moniker-end

<!---
> [!NOTE]  
> **Feature availability:** This feature is supported from VSTS or an on-premises TFS 2015.1 or later version.  
> 
--> 
<a id="reorder-cards"></a>
::: moniker range="vsts"
You can drag any work item to any column or swimlane on the Kanban board. You can even change the order of items as you move a card to a new column. 

![Reorder cards while changing columns](https://i3-vso.sec.s-msft.com/dynimg/IC822185.gif)
::: moniker-end

::: moniker range=">= tfs-2015 <= tfs-2018"
You can drag any work item to any column or swimlane on the Kanban board. You can even change the order of items as you move a card to a new column. (Requires TFS 2015.1 or later version.)  

![Reorder cards while changing columns](https://i3-vso.sec.s-msft.com/dynimg/IC822185.gif)
::: moniker-end

::: moniker range="vsts || >= tfs-2015 <= tfs-2018"
> [!TIP]
> You can drag-and-drop work items onto a sprint from any backlog or board. To add sprints to a team backlog, see [Set team defaults](../scale/set-team-defaults.md). 

::: moniker-end

<a id="card-reorder-setting"></a>

::: moniker range="vsts"
## Set card reordering team preference  

If you want to preserve the backlog priority when you move a card to a new column, you can change the Kanban board card reordering setting for your team. 

1. To open, click the ![gear icon](../_img/icons/team-settings-gear-icon.png) gear icon from your team's Kanban board.  

	<img src="_img/kanban-card-customize-open-settings.png" alt="Kanban board, open common configuration settings" style="border: 1px solid #C3C3C3;" />  

	If you're not a team admin, [get added as one](../scale/add-team-administrator.md). Only team and project admins can set team settings.  

2. From the Card reordering page you can choose between the two supported behaviors.    
	<img src="../kanban/_img/kanban-card-reordering-up1.png" alt="Kanban board, Card reording configuration dialog" style="border: 1px solid #C3C3C3;" />   

	The setting you choose applies to all active Kanban boards for your team.  
::: moniker-end


::: moniker range=">= tfs-2015 <= tfs-2018"
<a id="card-reorder-setting"></a>
## Set card reordering team preference  

If you want to preserve the backlog priority when you move a card to a new column, you can change the Kanban board card reordering setting for your team. (Requires TFS 2015.2 or later version.)

1. To open, click the ![gear icon](../_img/icons/team-settings-gear-icon.png) gear icon from your team's Kanban board.  

	<img src="_img/kanban-card-customize-open-settings.png" alt="Kanban board, open common configuration settings" style="border: 1px solid #C3C3C3;" />  

	If you're not a team admin, [get added as one](../scale/add-team-administrator.md). Only team and project admins can set team settings.  

2. From the Card reordering page you can choose between the two supported behaviors.    
	<img src="../kanban/_img/kanban-card-reordering-up1.png" alt="Kanban board, Card reording configuration dialog" style="border: 1px solid #C3C3C3;" />   

	The setting you choose applies to all active Kanban boards for your team.  
::: moniker-end

<a id="card-reorder-note"></a>
::: moniker range="vsts || >= tfs-2015 <= tfs-2018"
> [!NOTE]  
> The last column, typically the Closed or Done column, is always ordered by Closed Date with recently Closed showing at the top. In all other columns, cards are ordered by the backlog order or they are reorder based on the Card reordering setting selected.  
::: moniker-end



