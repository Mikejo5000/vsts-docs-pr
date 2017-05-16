---
title: Drive Git or TFVC development from a work item | Team Services & TFS 
description:  Associate or automatically link work items with source control branches, builds, commits, changesets, pull requests or other Git or TFVC supported operation  
ms.technology: vs-devops-agile-wit
ms.prod: vs-devops-alm
ms.assetid: BD7CE3C1-9E15-4BD6-B9CD-F78569C74D0D  
ms.manager: douge
ms.author: kaelli
ms.date: 04/05/2017  
---

#Drive Git development from a work item   

**Team Services | TFS 2017**   

>[!NOTE]  
><b>Feature availability: </b>The Development section appears in the work item web form for Team Services or TFS 2017 or later versions, configured with the [new work item tracking experience](../process/new-work-item-experience.md). It supports both Git and TFVC version control repositories. Go here to learn how to [add a Git repository for your existing team project](../../setup-admin/create-team-project.md#git-and-tfvs-repos).   

One of the ways your team can drive their development and stay in sync is to link your work items to the objects created during development, such as branches, commits, pull requests, and builds. You can begin that linking by creating a branch from one or more work items. Later, you can create pull requests, quickly open commits, and maintain a record of development operations performed to complete specific work.  

The Development section records all Git development processes that support completion of the work item. This section can show your team information needed to take the next development step and minimize navigational steps to accomplish common development tasks. It also supports traceability, providing visibility into all the branches, commits, pull requests, and builds related to the work item.    

<img src="_img/drive-git-development-dev-section.png" alt="Work item form, Development section" style="border: 1px solid #CCCCCC;" />  

From it, you can quickly access branches, pull requests, and commits which are linked to the work item. Also, you can initiate a pull request for a branch you've created or linked to from the work item.  

Links shown in this section appear as a result of these actions:   
- Creating a branch, commit, or pull request from the work item    
- Specifying the work item ID during a commit, pull request, or other supported Git or TFVC operation   
- Specifically linking the work item from the Development section or ![Links tab icon](_img/icon-links-tab-wi.png) Links tab to a source code branch, build, or other supported Git or TFVC operation.  

Hovering over any entry listed under the Development section activates the hyperlink to the associated object.    

The link types you can add within the development section are Branch, Build, Changeset, Commit, Found in build, Integrated in build, Pull Request, and Versioned Item. 

>[!NOTE]  
>The link types, **Found in build** and **Integrated in build** are only available from Team Services and only work with the current build processes (not XAML builds). 

<img src="../track/_img/link-tracking-artifact-to-artifact-link-types.png" alt="Artifact-to-artifact link types" style="border: 1px solid #CCCCCC;" /> 


<a id="git-development">  </a>
## Workflow process

Consider creating a new branch when there are no linked code artifacts. If there is a branch but no pull requests, consider creating a pull request. Here's a typical workflow sequence when working with a Git repository. 

1. Start work on the work item by creating a branch. You can add a new Git branch from within the Development section...  

	<img src="_img/linkscontrol-bug-form-dev-related-links.png" alt="Bug work item form, Agile process, Development and Related links controls" style="border: 1px solid #CCCCCC;" /> 
 
	... or, from the form's ![Actions icon](../_img/icons/actions-icon.png) Actions menu.  

	![Action menu, add new branch](_img/add-work-item-new-branch.png)  

	Name the branch and select the repository on which it's based.   

	![Create Git branch](_img/git-dev-create-branch.png)  

	Branches you create are automatically linked to the work item.  

	>[!NOTE]  
	>You can only create a branch once you've added files to the main branch, which is always named ```master```.   

2. From Visual Studio or other supported IDE, fetch the contents of the branch you just created. For details, see [Update code with fetch and pull, Download changes with fetch](../../git/tutorial/pulling.md#download-changes-with-fetch). (While any code editing and committing process will work, we work best with an edition of Visual Studio.)  

3. Add or modify files in the branch that you created.  

4. From Visual Studio or other supported IDE, commit and push changes from your local branch to the repository. By adding the work item ID to your commit, you automatically link the commit to the work item.   

	![Commit and push changes](_img/git-dev-commit-sync.png)  

	If this is the first time pushing changes from a new branch, you'll need to publish the branch before pushing your changes. For more details, see [Share code with push](../../git/tutorial/pushing.md).   

<a id="create-pull-request">  </a>
5. Create a [pull request](../../git/pull-requests.md). You create a pull request to merge the changes you made to a master branch and get your changes reviewed by other members of your team.  

	![Create pull request](_img/git-dev-create-pull-request.png)   

	>[!NOTE]
	>Once you've created a pull request, you can't create a new pull request for the same branch until you complete the previous pull request.     

6. Complete the pull request from the web portal or Visual Studio.  
 
	<img src="_img/git-dev-complete-pull-request.png" alt="Complete pull request" style="border: 1px solid #CCCCCC;" />

<a id="add-branch-multi-wi">  </a>
## Create a branch for several work items  

You can also add a new branch from the work item listed on the backlog or Kanban board without having to open the work item. Using [multi-select](create-your-backlog.md#bulk-modify), you can select several work items and create a new branch where they're all linked to the branch. 

For example, here we select 5 items to link to a new branch.  

![Select multiple items from backlog](_img/add-work-item-create-branch-multi-items-menu.png)

And, we specify the name of the branch.  

![create new branch dialog](_img/add-work-item-create-branch-multi-items.png)  



<a id="link-objects">  </a>
## Link to existing development and build objects

All items listed under the Development section also appear under the ![Links tab icon](_img/icon-links-tab-wi.png) Links tab. All development actions initiated from the Development section are also logged under the ![History tab icon](_img/icon-history-tab-wi.png) History tab. 

![Links tab, development links](_img/add-work-item-dev-links.png)  

To link a work item to an existing object, click the ![Add link](../_img/icons/add-link-icon.png) Add links icon and then choose the link type.  

![Select multiple items from backlog](_img/add-work-items-link-to-existing-branch.png)

[Link work items to support traceability](../track/link-work-items-support-traceability.md).   


### Remove a link 
If you want to remove a link, you can do so from the Development section by highlighting it first and then click the ![delete icon](../_img/icons/delete_icon.png) delete icon.  

![Development section, delete a link](_img/add-work-item-remove-dev-link.png)  

Or, you can select it from the ![Links tab icon](_img/icon-links-tab-wi.png) Links tab and click the ![delete icon](../_img/icons/delete-link.png).



## Related notes

Learn more about tracking work with work items and developing with Git from these resources: 

- [Add work items](add-work-items.md)  
- [Git overview](../../git/overview.md)  
- [TFVC overview](../../tfvc/overview.md)
- [Productivity tips](../productivity/productivity-tips.md)  
- [Link work items to support traceability and manage dependencies](../track/link-work-items-support-traceability.md)  
- [Create your backlog](create-your-backlog.md)  
- [Agile tools](../overview.md)  

>[!NOTE]    
>To learn more or to customize the Development links control, see [LinksControlOptions elements, Development links control](../reference/linkscontroloptions-xml-elements.md#development-links-control).    

Keep in mind that the Development section only appears when using the web portal for Team Services or TFS 2017 or later versions. The work item tracking experience and forms that appear in Visual Studio will be missing several of the features that the web portal makes available.  

### Associated work items in build 

With Git commits, any work items that have been linked to a commit will be listed under the Associated work items in the build summary page. 

<img src="_img/developer-associated-work-items-build.png" alt="Work item form, Development section" style="border: 1px solid #CCCCCC;" />  

<!--- Add info about option to set build linking; link to release notes if needed --> 

[!INCLUDE [temp](../_shared/help-support-shared.md)]  
