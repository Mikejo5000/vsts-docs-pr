---
title: Set personal or team favorites
titleSuffix: VSTS & TFS  
description: Quickly access artifacts by favoriting them in Visual Studio Team Services & Team Foundation Server
ms.technology: devops-collab
ms.prod: devops
ms.assetid: 473E452D-59F7-4F6F-97C6-657ECD99ADCB
ms.manager: douge
ms.author: kaelli
author: KathrynEE
ms.topic: tutorial
monikerRange: '>= tfs-2017'
ms.date: 07/21/2018
---

# Set personal or team favorites    

**VSTS | TFS 2018 | TFS 2017.1**  

By favoriting an artifact or view, you can quickly access it. An artifact is a specific container, definition, or configurtion of a feature or tool&mdash;such as a project, repository, build pipeline, or query. As your code base, work tracking efforts, developer operations, and organization grows, you'll want to be able to quickly navigate to those artifacts of interest to you and your team. Setting favorites allows you to do just that.  

You can set favorites for yourself or your team. Team favorites are a quick way for members of your team to quickly access shared resources of interest. You favorite an item for yourself by clicking the ![favorites](../../_img/icons/icon-favorite-star.png) star icon. The favorited item will then show up easily from one or more directory lists. You set favorites for a team through the context menu for the artifact. 

You can set favorites for the following artifacts from the indicated page. 

::: moniker range="vsts"

> [!div class="mx-tdCol2BreakAll"]        
> |Service/area |     Artifacts        | Page |
> |---------------|---------|---------| 
> | Organization & projects | Projects and teams | **Projects**  (personal favorites only)  |  
> | Dashboard | Team dashboards  | **Dashboards**  | 
> | Code | Repositories | **Code>Branches**  (personal favorites only) | 
> | Work, Agile tools for a team | Backlogs, boards, sprint backlogs, sprint taskboards | **Work>Queries** (requires enabling the [**New Navigation** or **New Navigation**](preview-features.md)) | 
> | Work  | Queries | **Work>Queries** |
> | Work | Delivery plans |  **Work>Plans** (personal favorites only, requires installation of the [Delivery Plans extension](../../boards/plans/review-team-plans.md)) | 
> | Build and Release | Pipeline definitions | **Build & Release>Build** or **Release**  | 
> | Test | Test plans | **Test>Test Plans** (personal favorites only) |


::: moniker-end

::: moniker range=">= tfs-2017 <= tfs-2018"


> [!div class="mx-tdCol2BreakAll"]  
> > |Service/area |  Artifacts  | Page |
> |---------------|---------|---------| 
> | Organization & projects | Projects and teams | **Projects**  (personal favorites only)  |  
> | Code | Repositories | **Code>Branches**  (personal favorites only) | 
> | Work  | Queries | **Work>Queries** |
> | Work | Delivery plans |  **Work>Plans** (personal favorites only, requires installation of the [Delivery Plans extension](../../boards/plans/review-team-plans.md)) | 
> | Build and Release | Pipeline definitions | **Build & Release>Build** or **Release**  | 
> | Test | Test plans | **Test>Test Plans** (personal favorites only) |

::: moniker-end



## Favorite a project or team  

[!INCLUDE [temp](../../_shared/new-navigation.md)] 


# [New navigation](#tab/new-nav)

::: moniker range="vsts"

0. To favorite a project, open the project **Summary** page and choose the ![favorites](../../_img/icons/icon-favorite-star.png) star icon.

	> [!div class="mx-imgBorder"]  
	> ![web portal, VSTS icon](_img/favorites/favorite-project-vert.png)  
<a id="team-artifact" />
0. To favorite a team artifact, open **Work>Backlogs** or **Work>Boards**. Select the team you want to favorite from the team selector and choose the ![](../../_img/icons/icon-favorite-star.png) star icon.

	> [!div class="mx-imgBorder"]  
	> ![Work>Boards, set team favorite](_img/favorites/set-team-favorite-vert.png)

0. To favorite other team artifacts, choose the ![](../../_img/icons/team.png) team icon, and then choose the ![](../../_img/icons/icon-favorite-star.png) star icon next to one of the listed artifacts. 

	> [!div class="mx-imgBorder"]  
	> ![Phone team work artifacts](_img/favorites/view-team-artifacts-vert.png) 

::: moniker-end

::: moniker range=">= tfs-2017  <= tfs-2018"
[!INCLUDE [temp](../../_shared/new-navigation-not-supported.md)]  
::: moniker-end


# [Previous navigation](#tab/previous-nav)

0. To favorite a project, open the project **Summary** page and choose the ![favorites](../../_img/icons/icon-favorite-star.png) star icon.

	> [!div class="mx-imgBorder"]  
	> ![web portal, VSTS icon](_img/favorites/favorite-project-horz-brn.png)

	Or, you can favorite a project from the **Projects** page by choosing the ![favorites](../../_img/icons/icon-favorite-star.png) star icon next to the project. 

---



<a id="view-favorites">  </a>
## View personal favorites   


# [New navigation](#tab/new-nav)

::: moniker range="vsts"

Access your favorites by choosing the ![](../../_img/icons/inbox.png) inbox icon, and then choosing **Favorites**. 

> [!div class="mx-imgBorder"]  
> ![View your favorited items](_img/favorites/open-favorites-page-vnav.png) 

::: moniker-end


::: moniker range=">= tfs-2017  <= tfs-2018"
[!INCLUDE [temp](../../_shared/new-navigation-not-supported.md)]  
::: moniker-end


# [Previous navigation](#tab/previous-nav)

From your Projects page, choose **My Favorites** to quickly access any artifact or item that you've marked as a favorite. 

> [!div class="mx-imgBorder"]  
> ![Account home, Favorites page](_img/favorites/project-page-favorites-horz.png)   

---


::: moniker range="vsts"
## Favorite an Agile tool 
::: moniker-end

# [New navigation](#tab/new-nav)

::: moniker range="vsts"

You can favorite several Agile tools for a team from a **Work** page.  

1. From **Work**, choose the page of interest, such as **Boards**, **Backlogs**, or **Sprints**.  

	For example, here we choose (1) **Work** and then (2) **Backlogs**.

	> [!div class="mx-imgBorder"]  
	> ![Open Work, Backlogs](_img/favorites/open-work-backlogs-vert.png)  

	To choose a specific team backlog, open the selector and select a different team or choose the ![home-icon](../../_img/icons/home-icon.png) **Browse all team backlogs** option. Or, you can enter a keyword in the search box to filter the list of team backlogs for the project.

	> [!div class="mx-imgBorder"]  
	> ![Choose another team](../../boards/sprints/_img/assign-items-sprint/team-selector-backlogs-agile.png) 

2.  Choose the ![](../../_img/icons/icon-favorite-star.png) star icon to favorite a team backlog. Favorited artifacts (![](../../_img/icons/icon-favorited.png) favorited icon) appear appear on your **Favorites** page and towards the top of the team backlog selector menu.

::: moniker-end

::: moniker range=">= tfs-2017  <= tfs-2018"
[!INCLUDE [temp](../../_shared/new-navigation-not-supported.md)]  
::: moniker-end

# [Previous navigation](#tab/previous-nav)

Favoriting a product backlog, sprint backlog, or Kanban board isn't supported in  previous navigation.  

---

::: moniker range="vsts"  
## Favorite a dashboard 
::: moniker-end

# [New navigation](#tab/new-nav)

::: moniker range="vsts"  

1. From **Overview>Dashboards**, open the selector and choose the **Browse all dashboards** option. 
 
	> [!div class="mx-imgBorder"]  
	> ![Dashboards, Browse all dashboards option](../../report/dashboards/_img/dashboards/browse-all-dashboards.png)  

2. The **Mine** page shows your favorited dashboards, and all dashboards of teams that you belong to. The **All** page (shown below) lists all dashboards defined for the project in alphabetical order. You can filter the list by team or by keyword.   
 
	> [!div class="mx-imgBorder"]  
	> ![Dashboards, Browse all dashboards option](../../report/dashboards/_img/dashboards/all-dashboards-list.png)  

	> [!TIP]
	> You can change the sort order of the list by choosing the column label.   
	 
3. To favorite a dashboard, hover over the dashboard and choose the ![star icon](../../_img/icons/icon-favorite-star.png).  

	> [!div class="mx-imgBorder"]  
	> ![Dashboards, Browse all dashboards option](../../report/dashboards/_img/dashboards/favorite-dashboard.png)  

	Favoriting a dashboard will cause it to appear on your **Favorites** page and towards the top in the **Dashboards** selection menu.
   
::: moniker-end  

::: moniker range=">= tfs-2017  <= tfs-2018"  
[!INCLUDE [temp](../../_shared/new-navigation-not-supported.md)]  
::: moniker-end  

# [Previous navigation](#tab/previous-nav)

Favoriting a dashboard isn't supported in previous navigation.  

---

## Favorite a repository

# [New navigation](#tab/new-nav)

::: moniker range="vsts"  

From any **Code** page, open the repository selector and choose the ![](../../_img/icons/icon-favorite-star.png) star icon for the repository you want to favorite.

> [!div class="mx-imgBorder"]  
> ![Code page, Repository selector, choose favorites icon](_img/favorites/favorite-repo-vert.png)  

::: moniker-end

::: moniker range=">= tfs-2017  <= tfs-2018"  
[!INCLUDE [temp](../../_shared/new-navigation-not-supported.md)]  
::: moniker-end  

# [Previous navigation](#tab/previous-nav)

From any **Code** page, open the repository selector and choose the ![](../../_img/icons/icon-favorite-star.png) star icon next to the repository you want to favorite. 

> [!div class="mx-imgBorder"]  
> ![Web portal, Code, Favorite a repo](_img/set-favorites-repository.png) 

---


## Favorite a build pipeline  

# [New navigation](#tab/new-nav)

::: moniker range="vsts"  

Open **Build and Release>Builds** and choose either **Mine** or **Definitions** page. Choose the ![](../../_img/icons/icon-favorite-star.png) star icon next to the build definition you want to favorite. Or, open the context menu of the build definition, and then select **Add to my favorites** or **Add to team favorites**.  

> [!div class="mx-imgBorder"]  
> ![Build & Release, Builds, Add to my favorites or team favorites, new navigation](_img/favorites/set-build-favorites-vert.png)

::: moniker-end

::: moniker range=">= tfs-2017  <= tfs-2018"  
[!INCLUDE [temp](../../_shared/new-navigation-not-supported.md)]  
::: moniker-end  

# [Previous navigation](#tab/previous-nav)

Open **Build and Release>Builds** and choose either **Mine** or **Definitions** page. Choose the ![](../../_img/icons/icon-favorite-star.png) star icon next to the build definition you want to favorite. Or, open the context menu of the build definition, and then select **Add to my favorites** or **Add to team favorites**.  

> [!div class="mx-imgBorder"]  
> ![Build & Release, Builds, Add to my favorites or team favorites, previous navigation](_img/favorites/set-favorites-build-definitions.png)


---

## Favorite a shared query 

# [New navigation](#tab/new-nav)  

::: moniker range="vsts"  

Open **Work>Queries** and choose the **All** page. Expand a folder as needed. Choose the ![](../../_img/icons/icon-favorite-star.png) star icon next to the query you want to favorite. 

Or, open the context menu of the query, and then select **Add to Team Favorites**, and then select from the list of teams. 

> [!div class="mx-imgBorder"]  
> ![Work>Queries, Add to favorites, new navigation](_img/favorites/favorite-query.png)

You can also set a query as a personal favorite by opening the query and choosing the ![](../../_img/icons/icon-favorite-star.png) star icon.

> [!div class="mx-imgBorder"]  
> ![Work>Queries, set shared query as a personal favorite](_img/favorites/set-query-favorite-personal.png) 

::: moniker-end

::: moniker range=">= tfs-2017  <= tfs-2018"  
[!INCLUDE [temp](../../_shared/new-navigation-not-supported.md)]  
::: moniker-end  

# [Previous navigation](#tab/previous-nav)

::: moniker range="vsts"

Open **Work>Queries** and choose the **All** page. Expand a folder as needed. Choose the ![](../../_img/icons/icon-favorite-star.png) star icon next to the query you want to favorite. 

Or, open the context menu of the query, and then select **Add to Team Favorites**, and then select from the list of teams. 

> [!div class="mx-imgBorder"]  
> ![Work>Queries, Add to favorites, new navigation](_img/favorites/favorite-query.png)

You can also set a query as a personal favorite by opening the query and choosing the ![](../../_img/icons/icon-favorite-star.png) star icon.

> [!div class="mx-imgBorder"]  
> ![Work>Queries, set shared query as a personal favorite](_img/favorites/set-query-favorite-personal.png) 

::: moniker-end

::: moniker range=">= tfs-2017 <= tfs-2018"

Open **Work>Queries**. Next, open the ![](../../_img/icons/actions-icon.png) actions icon menu of the shared query you want to favorite, and then select **Add to my favorites** or **Add to team favorites**.  

![Web portal, Work, Queries, Add to my favorites](_img/set-favorites-shared-query.png)


::: moniker-end

---

## Favorite a delivery plan 

To mark a delivery plan as a favorite, open the **Work>Plans** page and choose the ![](../../_img/icons/icon-favorite-star.png) star icon next to the Delivery Plan.

## Favorite a test plan    

To mark a test plan as a favorite, open the **Test>Test Plans** page and choose the ![](../../_img/icons/icon-favorite-star.png) star icon next to a test plan from the menu that shows All test plans. 


<a id="unfavorite">  </a>
## Unfavorite an artifact


# [New navigation](#tab/new-nav)  

::: moniker range="vsts"  

You can unfavorite an artifact from your **Favorites** page. Choose the ![](../../_img/icons/inbox.png) inbox icon, and then choose **Favorites**. Choose the ![](../../_img/icons/icon-favorited.png) favorited icon of a currently favorited artifact. 

> [!div class="mx-imgBorder"]  
> ![View your favorited items](_img/favorites/open-favorites-page-vnav.png) 

Similarly, you can unfavorite an artifact from the same page where you favorited it. 

::: moniker-end

::: moniker range=">= tfs-2017  <= tfs-2018"  
[!INCLUDE [temp](../../_shared/new-navigation-not-supported.md)]  
::: moniker-end  

# [Previous navigation](#tab/previous-nav)

You can unfavorite an artifact from the **Projects>Favorites** page and choose the ![](../../_img/icons/icon-favorited.png) favorited icon of a currently favorited artifact. 

Similarly, you can unfavorite an artifact from the same page where you favorited it. 


---



<!---
<a id="team-favorites"> </a>
## Set team favorites 
 You can define team favorites for the following:

- **Code/Explorer**: Add repos or folders to team favories  
- **Work/Queries**: A  [Shared work item queries](../../boards/queries/using-queries.md) to team favorites    
- **Build/Explorer**: Add build definitions to team favorites   

From your team context, drag shared queries, builds, and folders to Team favorites to provide quick access to those items. Or, choose the Add to team favorites option from the context menu for the item. You must be [added as a team admin](../../organizations/settings/add-team-administrator.md) to manage team favorites.  

![Drag items to team favorites](../../_img/alm-index-team-favorites.png)  

-->


## Related articles

- [Manage personal notifications](../../notifications/howto-manage-personal-notifications.md) 
- [Set your preferences](../../organizations/settings/set-your-preferences.md) 