---
title: Switch team project or team context 
titleSuffix: VSTS & TFS  
description: Change the focus of your view to another team project or team Visual Studio Team Services (VSTS) and Team Foundation Server (TFS)  
ms.technology: vs-devops-wit
ms.prod: vs-devops-alm
ms.assetid:  
ms.manager: douge
ms.author: kaelli
ms.date: 02-24-2018
---


# Switch team project or team focus   

[!INCLUDE [temp](../_shared/version-vsts-tfs-all-versions.md)]

<a id="switch-team-context">  </a>

Several features depend on the team project or team that you have selected. For example, dashboards, backlogs, and board views will change depending on the context selected. 

For example, when you add a work item, the system references the default area and iteration paths defined for the team context. Work items you add from the team dashboard (new work item widget) and queries page are assigned the team default iteration. Work items you add from a team backlog or board, are assigned the team default backlog iteration. To change team defaults, see [Set team defaults](../work/scale/set-team-defaults.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json).  

You navigate to your team context from the top navigation bar. The method changes slightly depending on the platform/version you work from.     

## View teams   

To view a list of teams defined for a team project, open the admin context for the team project, and choose **Overview**.  

>[!NOTE]  
>**Feature availability**: The **Change process** link is only supported for team projects that use the [Inheritance process model](../work/customize/inheritance-process-model.md).  

<img src="../work/scale/_img/multiple-teams-view-teams.png" alt="Web portal, admin context, team project, Overview page" style="border: 2px solid #C3C3C3;" /> 


<a id="projects">  </a>
## Projects: Navigate to a team project 
From the **Projects** page you can quickly navigate to a team project or a team that you've accessed or worked in previously. Projects are listed in the order you've last accessed, with the most recent five projects accessed appearing first. All projects you've accessed are listed within the **All** section.  

<img src="../user-guide/_img/account-home-projects.png" alt="Account home, Projects page" style="border: 1px solid #CCCCCC;" />

As you hover over the project, you can click one of the links to go to the Home (dashboards), Code, Work, Build & Release, or Test hub of the team project. Click the ![favorites](../_img/icons/icon-favorite-star.png) star icon to mark the team project as a favorite. 

<img src="../user-guide/_img/account-home-projects-hover-links.png" alt="Account home, Projects page, hover over a team project" style="border: 1px solid #CCCCCC;" />    

### Filter projects and teams
If a project isn't listed, you can find it by searching for it using the *Filter projects and teams* search box. Simply type a keyword contained within the name of a team project or team. Here we type **Design** to find the Contoso project Design team. 

<img src="../user-guide/_img/account-home-search-projects-design.png" alt="Account home, Projects page, filter on Design" style="border: 1px solid #CCCCCC;" />    

### Add a team project
If you're an account administrator or are a member of the Project Collection Administrators group, the New Project button is shown. Click New Project to [add a team project](../accounts/create-team-project.md). 

<img src="../user-guide/_img/account-home-projects-new-project.png" alt="Account home, Projects page, New team project" style="border: 1px solid #CCCCCC;" />


## Switch to a different team 

>[!NOTE]  
>**Feature availability**: The Account Landing Page feature is in preview mode for VSTS and enabled for all users from web portal for TFS 2017.1 and later versions. To learn more about this feature, see [Work effectively from your account hub](../user-guide/account-home-pages.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json). To enable or disable the feature, see [Enable preview features](../collaborate/preview-features.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json).   

 


### VSTS
<a id="switch-context-team-services" />
 
You can switch your team focus to a team project or team you've recently viewed from the team project/team drop-down menu. If you don't see the team or team project you want, click **Browse&hellip;** or click the ![VSTS icon](../settings/_img/switch-team-focus-account-project-page-icon.png) VSTS icon to [access your account hub and browse all team projects and teams](../user-guide/account-home-pages.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json). If you haven't yet enabled the Account Landing Page, you'll be taken to the account home page. 

To go directly to the [project vision and status page](../collaborate/project-vision-status.md), choose the project home icon from the drop-down menu, for example, ![project home icon](../_shared/_img/work-web-portal-home-page-icon.png).

<img src="../_shared/_img/work-web-portal-ts-switch-team-focus.png" alt="Choose another team from the team project menu" style="border: 2px solid #C3C3C3;" /> 

### TFS 2017.1 
<a id="switch-context-tfs-2017-1" /> 

To switch your team focus to a team project or team you've recently viewed, hover over the ![VSTS icon](../settings/_img/switch-team-focus-account-project-page-icon.png) VSTS icon and choose from the drop-down menu of options. If you don't see the team or team project you want, choose **Browse&hellip;** to [browse all team projects and teams](../user-guide/account-home-pages.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json). Your selection will open the [project vision and status page](../collaborate/project-vision-status.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json) for the team project.

To access your [account hub](../user-guide/account-home-pages.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json), click the ![VSTS icon](../settings/_img/switch-team-focus-account-project-page-icon.png) VSTS icon. If you haven't yet enabled the Account Landing Page, you'll be taken to the account home page.  

To go directly to the [project vision and status page](../collaborate/project-vision-status.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json), choose the project home icon from the drop-down menu, for example, ![project home icon](../_shared/_img/work-web-portal-home-page-icon.png).

<img src="../_shared/_img/work-web-portal-tfs-2017-1-switch-team-focus.png" alt="Choose another team from the team project menu" style="border: 2px solid #C3C3C3;" /> 


### TFS 2017
<a id="tfs-2017-switch-context" /> 

Open the team project/team drop-down menu and select the team project/team that you've recently visited. If you don't see the team or team project you want, choose **Browse all** to browse all team projects and teams. 

<img src="../_shared/_img/switch-context-tfs-2017.png" alt="Choose another team from the team project menu" style="border: 2px solid #C3C3C3;" /> 


### TFS 2015
<a id="tfs-2015-switch-context" />

Open the team project/team drop-down menu and select the team project/team that you've recently visited. If you don't see the team or team project you want, choose **Browse all** to browse all team projects and teams. 

<img src="../_shared/_img/switch-team-project-2.png" alt="Choose another team from the team project menu" style="border: 2px solid #C3C3C3;" /> 


## Switch to a team project or team from the account hub 
If you work in VSTS and TFS 2017.1, you can use your account hub to view and quickly navigate to teams, team projects, branches, work items, pull requests and other objects that are relevant to you. For details, see [Work effectively from your account hub](../user-guide/account-home-pages.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json).  



## Related content
- [Work effectively from your account hub](../user-guide/account-home-pages.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json)
- [Add teams and team members](../work/scale/multiple-teams.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json)