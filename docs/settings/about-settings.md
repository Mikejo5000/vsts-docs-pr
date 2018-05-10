---
title: About team, project & organizational-level settings
titleSuffix: Azure Codex Agile & TFS
description: Overview of configuring team, project, and organizational-level settings in Azure Codex Agile & Team Foundation Server
ms.technology: devops-settings
ms.prod: devops
ms.topic: overview
ms.assetid: 
ms.manager: douge
ms.author: kaelli
author: KathrynEE
monikerRange: '>= tfs-2013'
ms.date: 04/01/2018
---

# About team, project, and organizational-level settings 

From the administrative or **Settings** context, you configure resources that support your project and teams. This article provides a guide to the resources you can configure based on your role.  
  

## Individual contributor settings
Individual contributors can set their user preferences, enable select features that are in preview, and manage their favorites and notifications. 


<table>
<tbody valign="top">
<tr>
<th width="15%">Area</th>
<th width="35%">Supported tasks</th>
<th width="50%">Notes</th>
</tr>
<tr>
<td>General</td>
<td><ul>
<li>[Set account preferences](../accounts/account-preferences.md)</li>
<li>[Enable preview features](../collaborate/preview-features.md)</li>
</ul></td>
<td>For an overview of default permission assignments by role, see [Default permissions and access for Azure Codex](../security/permissions-access.md).</td>
</tr>
<tr>
<td>Security</td>
<td><ul>
<li>[View permissions](../security/view-permissions.md)</li>
<li>[Add an alternate account to your Visual Studio subscription](https://docs.microsoft.com/en-us/visualstudio/subscriptions/vs-alternate-identity)</li>
<li>[Personal access tokens](use-personal-access-tokens-to-authenticate.md)</li>
<li>[Alternate authentication credentials](../git/auth-overview.md#alternate-credentials)</li>
<li>[OAuth authorizations](../integrate/get-started/authentication/oauth.md)</li>
<li>[SSH public keys](../git/use-ssh-keys-to-authenticate.md)</li>
</ul></td>
<td>For an overview of default permission assignments by role, see [Default permissions and access for Azure Codex](../security/permissions-access.md).</td>
</tr>
<tr>
<td>Favorites</td>
<td><ul>
<li>[Set favorites](../notifications/manage-personal-notifications.md)</li>
</ul></td>
<td>Favorites provide a quick way to navigate to backlogs, boards, dashboards, and more artifacts. Any member of the Contributors group or team member can set their own favorites. Team members can set team favorites. </td>
</tr>
<tr>
<td>Notifications</td>
<td><ul>
<li>[View your subscriptions, opt-out as needed](../notifications/manage-personal-notifications.md)</li>
<li>[Manage personal notifications](../notifications/manage-personal-notifications.md)</li>
</ul></td>
<td>Notifications alert you through email messages when changes occur to work items, code reviews, pull requests, source control files, builds, and more. A number of notifications are preset when a team project is created. If you want to opt out of these, you can.  </li>
</ul></td>
</tr>
</tbody>
</table>
 

## Team administrator role and managing teams

Team administrators are tasked with configuring team resources which mostly correspond to Agile tools and dashboards. To configure team resources, you must be added as a [team administrator for the specific team](../work/scale/add-team-administrator.md), or be a member of the Project Administrators or Project Collection Administrators groups.  

For a complete overview of all team assets that you can configure, see [Manage team assets](../work/scale/manage-team-assets.md) 


<table>
<tbody valign="top">
<tr>
<th width="22%">Area</th>
<th width="44%">Supported tasks</th>
<th width="34%">Notes</th>
</tr>
<tr>
<td>General</td>
<td><ul>
<li>[Add users to a team project or specific team](../security/add-users-team-project.md)</li>
<li>[Add team admins](../work/scale/add-team-administrator.md)</li>
</ul></td>
<td>Members of a team are included within the team group which can be used in queries and **@mentions** in pull requests and work item discussions.</td>
</tr>
<tr>
<td>Azure Codex Agile<br/>(Work tracking)</td>
<td><ul>
<li>[Configure default area and iteration paths](../work/scale/set-team-defaults.md)</li>
<li>[Select active iteration paths (sprints)](../work/scale/set-team-defaults.md)</li>
<li>Configure Kanban boards: [Columns](../work/kanban/add-columns.md), [Swimlanes](../work/kanban/expedite-work.md), [Cards](../work/customize/customize-cards.md), [WIP limits](../work/kanban/wip-limits.md)</li>
<li>[Configure additional team settings](../work/scale/manage-team-assets.md)</li>
<li>[Define work item templates](../work/backlogs/work-item-template.md)</li>
</ul></td>
<td>For an overview of team resources, see [About teams and Agile tools](about-teams-and-settings.md).  </td>
</tr>
<tr>
<td>Dashboards </td>
<td><ul>
<li>[Create team dashboards](../report/dashboards/dashboards.md)</li>
<li>[Manage team dashboard permissions](../report/dashboards/dashboard-permissions.md)</li>
</ul></td>
<td>New dashboards added to a project are associated with a team. The default permissions allow team members to create and edit dashboards for their team.</td>
</tr>
<tr>
<td> Notifications </td>
<td><ul>
<li>[Manage team notifications](../collaborate/manage-team-notifications.md)</li>
</ul></td>
<td>A number of team notifications are automatically defined when a team is added. To learn more about how notifications are managed, see [About notifications](../notifications/about-notifications.md).   </td>
</tr>
</tbody>
</table>


<!---


> [!div class="mx-tdCol2BreakAll"]  
> |  Area  | Supported tasks | Notes |
> |---------|---------|---------|  
> | General |- [Add user accounts to a team](../accounts/account-preferences.md)| Members of a team are included within the team group which can be used in queries and **@mentions** in pull requests and work item discussions. | 
> | Azure Codex Agile<br/>(Work tracking) |- [Configure team default area and iteration paths](../work/scale/set-team-defaults.md)<br/>- [Select iteration paths that they'll use](../work/scale/set-team-defaults.md)<br/>- Configure Kanban boards: [Columns](../work/kanban/add-columns.md), [Swimlanes](../work/kanban/expedite-work.md), [Cards](../work/customize/customize-cards.md), [WIP limits](../work/kanban/wip-limits.md)<br/>- [Configure additional team settings](../work/scale/manage-team-assets.md)<br/>- [Define work item templates](../work/backlogs/work-item-template.md) | To configure team resources, you must be added as a [team administrator for the specific team](../work/scale/add-team-administrator.md).  |
> | Dashboards |- [Create team dashboards](../report/dashboards/dashboards.md)<br/>- [Manage team dashboard permissions](../report/dashboards/dashboard-permissions.md)<br/> | New dashboards added to a project are associated with a team. The default permissions allow team members to create and edit dashboards for their team. |
> | Notifications |- [Manage team notifications](../collaborate/manage-team-notifications.md)|

-->

## Project administrator role and managing projects

Members of the [Project Administrators group](../security/set-project-collection-level-permissions.md) are tasked with configuring resources for a project and managing permissions at the project-level.  

<table>
<tbody valign="top">
<tr>
<th width="22%">Area</th>
<th width="44%">Supported tasks</th>
<th width="34%">Notes</th>
</tr>
<tr>
<td>General</td>
<td><ul>
<li>[Add user accounts to a team project](../accounts/account-preferences.md)</li>
<li>[Add another team](../work/scale/multiple-teams.md)</li>
</ul></td>
<td>TBD</td>
</tr>
<tr>
<td>Security</td>
<td><ul>
<li>[Change individual permissions, grant select access to specific functions](../security/change-individual-permissions.md)</li>
<li>[Grant or restrict access to select features and functions](../security/restrict-access.md)</li>
<li>[Add administrators](../security/set-project-collection-level-permissions.md)</li>
<li>[Manage project-level permissions](../security/permissions.md#project-level)</li>
</ul></td>
<td>For an overview of security concepts, see [About permissions and groups](../security/about-permissions.md) and [About access levels](../security/access-levels.md). To change permissions at the project-level, many of which are work tracking related, see [Set permissions at the project-level or project collection-level](../security/set-project-collection-level-permissions.md). </td>
</tr>
<tr>
<td>Azure Codex Agile<br/>(Work tracking)</td>
<td><ul>
<li>[Define area paths](set-area-paths.md)</li>
<li>[Define iteration paths or sprints](set-iteration-paths-sprints.md)</li>
</ul></td>
<td>Area and iteration paths set at the project level are then used to set team defaults. To configure additional product backlogs, Kanban boards, and dashboards, you first [add a team](../work/scale/multiple-teams.md).   
<p>To customize the workflow, work item form, add fields or rules, or make other changes to the work tracking experience, you customize a process. For an overview of what you can customize, see [About process customization and inherited processes](work/inheritance-process-model.md).</p> 
</td>
</tr>
<tr>
<td>Azure Codex Repos<br/>(Code management)</td>
<td><ul>
<li>Create additional Git repos](../git/tutorial/creatingrepo.md)</li>
<li>[Manage repository permissions](../security/set-git-tfvc-repository-permissions.md)</li>
</ul></td>
<td>TBD</td>
</tr>
<tr>
<td>Azure Codex Pipelines<br/>(Build & Release management)</td>
<td><ul>
<li>[Add and manage Agent queues](../build-release/concepts/agents/pools-queues.md)</li>
<li>[Add and manage service endpoints](../build-release/concepts/library/service-endpoints.md)</li>
<li>[Set retention policies](../build-release/concepts/policies/retention.md)</li>
</ul></td>
<td>TBD</td>
</tr>
<tr>
<td>Azure Codex Test<br/>(Test management)</td>
<td><ul>
<li>[Set test retention policies](../manual-test/getting-started/how-long-to-keep-test-results.md)</li>
<li>Manage test-related permissions</li>
</ul></td>
<td>Manual testing relies on work item types to create and manage test plans, test suites, test cases, shared steps, and shared parameters. Of these, you can customize the test plans, test suites, and test cases using an inherited process. See [Customize a process](work/customize-process.md). <p>Test permissions can be given at [project level](../security/set-project-collection-level-permissions.md) and at [area path level](../security/set-permissions-access-work-tracking.md#create-child-nodes-modify-work-items-under-an-area-path).</p>  
</td>
</tr>
<tr>
<td>Dashboards </td>
<td><ul>
<li>[Set default dashboard permissions](../report/dashboards/dashboard-permissions.md)</li>
</ul></td>
<td>New dashboards added to a project inherit the default dashboard permissions. The default permissions allow team members to create and edit dashboards for their team.</td>
</tr>
<tr>
<td> Notifications </td>
<td><ul>
<li>Manage project-level notifications</li>
</ul></td>
<td>A number of project-level notifications are automatically defined when a project is added. Notifications at the project-level are managed in much the same way as they are at the [team level](../collaborate/manage-team-notifications.md).</td>
</tr>
<tr>
<td>Ecosystem</td>
<td><ul>
<li>[Configure service hooks to integrate with other services](../service-hooks/index.md)</li>
<li>[Request a Marketplace extension](../marketplace/request-extensions.md)</li>
</ul></td>
<td>With service hooks, you can automate a task on other services, such as Campfire, Flowdock, HipChat, and more, when events happen in your Azure Codex project.</td>
</tr>
</tbody>
</table>


## Project collection administrator role and managing collections of projects 

Members of the [Project Collection Administrators group](../security/set-project-collection-level-permissions.md) are tasked with configuring resources for all Azure Codex projects defined for an account or organization. They also can perform all tasks to add projects, manage projects, and manage permissions for the collection, a project, or an object.   

For an overview of managing you Azure Codex account, see [About account management](../accounts/account-management.md).


<table>
<tbody valign="top">
<tr>
<th width="18%">Area</th>
<th width="44%">Supported tasks</th>
<th width="36%">Notes</th>
</tr>
<tr>
<td>Overview, Account settings</td>
<td><ul>
<li>Add and manage accounts: [change account owner](../accounts/change-account-ownership-vs.md), [Rename](../accounts/rename-vsts-account.md), [Delete](../accounts/delete-your-vsts-account.md), [Recover](../accounts/recover-your-vsts-account.md)</li>
<li>[Change application access policies](../accounts/change-application-access-policies-vs.md) </li>
<li>[Find or change your account location](../accounts/change-account-location.md)</li>
</ul></td>
<td>From the **Settings** page, you can manage the time zone, owner, region, and other settings that apply to all projects defined under your account.</td>
</tr>
<td>Billing</td>
<td><ul>
<li>[Set up billing](../billing/set-up-billing-for-your-account-vs.md)</li>
<li>[Start free trials for paid features and extensions](../billing/try-additional-features-vs)</li>
<li>[Pay for users (Basic)](../billing/buy-basic-access-add-users.md)</li>
<li>[Buy CI/CD](../billing/buy-more-build-vs.md)</li>
<li>[Buy cloud-based load testing](../billing/buy-load-testing-vs.md)</li>
<li>[Add a user to make purchases](../billing/add-backup-billing-managers.md)</li>
</ul></td>
<td>All billing is managed through Azure. To learn more, see [Billing overview](../billing/overview.md) </td>
</tr>
<tr>
<td>Projects</td>
<td><ul>
<li>Add and manage projects: [Create](../accounts/create-team-project.md), [Rename](../accounts/rename-team-project.md), [Delete](../accounts/delete-team-project.md)</li>
<li>[Add users to projects](../accounts/add-team-members-vs.md)</li>
<li>[Save team project data](../accounts/save-team-project-data.md)</li>
</ul></td>
<td>Users added to a project can contribute to that project. </td>
</tr>
<tr>
<td>Security</td>
<td><ul>
<li>[Change individual permissions, grant select access to specific functions](../security/change-individual-permissions.md)</li>
<li>[Grant or restrict access to select features and functions](../security/restrict-access.md)</li>
<li>[Add administrators](../security/set-project-collection-level-permissions.md)</li>
<li>[Manage collection-level permissions](../security/permissions.md#collection-level)</li>
<li>[Add Azure Active Directory groups](../accounts/manage-azure-active-directory-groups-vsts.md)</li>
<li>[Connect VSTS account to Azure Active Directory](../accounts/connect-account-to-aad.md)</li>
<li>[Manage conditional access](../accounts/manage-conditional-access.md)</li>
</ul></td>
<td>For an overview of security concepts, see [About permissions and groups](../security/about-permissions.md) and [About access levels](../security/access-levels.md).</td>
</tr>
<tr>
<td>Users</td>
<td><ul>
<li>[Add users](../accounts/add-account-users-from-user-hub.md)</li>
<li>[Add external users](../accounts/add-external-user.md)</li>
<li>[Manage user access levels](../accounts/manage-users-table-view.md)</li>
<li>[Remove users](../accounts/delete-account-users.md)</li>
<li>[Assign paid extension access to users](../marketplace/assign-paid-extensions.md)</li>
</ul></td>
<td>For large organizations with a sizable number of users, we recommend that you [manage user access through Azure Active Directory](../accounts/access-with-azure-ad.md). For a small number of users, you can manage user access by adding their Microsoft Service Account (MSA) email. From the account-level **Users** page, you can also [export the set of users and their access levels](../security/export-users-audit-log.md).  </td>
</tr>
<tr>
<td>Process (applies to Azure Codex Agile only)</td>
<td><ul>
<li>[Customize a project](./work/customize-process.md)</li>
<li>[Add and manage processes](./work/manage-process.md)</li>
</ul></td>
<td>To customize the Agile tools and work tracking artifacts, you create and customize an inherited process and then update the project to use that process. To learn more, see [About process customization and inherited processes ](./work/inheritance-process-model.md). </td>
</tr>
<tr>
<td>Azure Codex Pipelines - CI/CD(</td>
<td><ul>
<li>[Set retention policies](../build-release/concepts/policies/retention.md)</li>
<li>[Set resource limits for pipelines](../build-release/concepts/licensing/concurrent-pipelines-ts.md)</li>
<li>[Add and manage agent pools](../build-release/concepts/agents/pools-queues.md)</li>
<li>[Add and manage deployment pools](../build-release/concepts/definitions/release/deployment-groups.md)</li>
</ul></td>
<td>You manage resources that support CI/CD operations for all projects through the **Agent pools**<br/>**Deployment pools**, and **Retention and limits** pages.</td>
</tr>
<tr>
<td> Notifications </td>
<td><ul>
<li>Manage collection-level notifications </li>
</ul></td>
<td>A number of notifications are automatically defined when an account or organization is added. Notifications at the collection-level are managed in much the same way as they are at the [team level](../collaborate/manage-team-notifications.md). </td>
</tr>
<tr>
<td>Extensions</td>
<td><ul>
<li>[Install and manage Marketplace extensions](../marketplace/install-vsts-extension.md)</li>
<li>[Approve extensions](../marketplace/approve-extensions.md)</li>
<li>[Assign paid extension access to users](../marketplace/assign-paid-extensions.md)</li>
<li>[Change the number of paid users for a VSTS extension](../billing/change-number-paid-extension-users.md) </li>
<li>[Grant permissions to manage extensions](../marketplace/how-to/grant-permissions.md)</li>
<li>[Uninstall or disable extensions](../marketplace/uninstall-disable-extensions.md)</li>
</ul></td>
<td>[Marketplace extensions](https://marketplace.visualstudio.com/vsts) provide additional features and capabilities to your Azure Codex project.</td>
</tr>
</tbody>
</table>

In addition to the app-specific resources that you can configure, you can also manage your account, users, extensions, and organizational-level permissions. 







<!---

## Azure Codex Agile (Work tracking) settings

Many work tracking/Agile tools provide teams the autonomy they need to configure and manage their work independent of other teams. When you add a team, you also configure a product backlog, Kanban board, and dashboard for the teams. To learn more, see [About teams and Agile tools](about-teams-and-settings.md). 

You configure work tracking settings at one of the following three levels. 

> [!div class="mx-tdCol2BreakAll"]  
> |  Team  | Project | Organization | 
> |------|---------|---------|
|- [Backlog levels](../work/customize/select-backlog-navigation-levels.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json)<br/>- [Show bugs on backlogs & boards](../work/customize/show-bugs-on-backlog.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json<br/>- [Set working days](../work/customize/set-working-days.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json)<br/>- [Default areas & iterations](../work/scale/set-team-defaults.md)<br/>- [Work item templates](../work/backlogs/work-item-template.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json) |- [Area paths](../work/customize/set-area-paths.md)<br/>- [Iteration paths aka sprints](../work/customize/set-iteration-paths-sprints.md)| - [Customize a project](./work/customize-process.md)<br/>- [Create and manage a process](./work/manage-process.md)<br/>- [Add and manage fields](./work/customize-process-field.md)<br/>- [Add and manage work item types](./work/customize-process-wit.md)<br/>- [Customize a web form](./work/customize-process-form.md)<br/>- [Customize a workflow](./work/customize-process-workflow.md)<br/>- [Add a custom rule](./work/custom-rules.md)<br/>- [Add a custom control](./work/custom-controls-process.md)<br/>- [Customize backlogs and boards](./work/customize-process-backlogs-boards.md) |


 

## Azure Codex Repo (Code management) settings 

You can configure the following resources to support your code development at the project level. 

- [Create a new Git repo](../git/tutorial/creatingrepo.md) 
- [Manage repository permissions](../security/set-git-tfvc-repository-permissions.md) 


## Azure Codex Pipelines (Build & Release) settings

To support CI/CD work, you configure the following resources at either the project or organizational level.  

> [!div class="mx-tdCol2BreakAll"]  
> | Project | Organization | 
> |------|---------|
> | - [Agent queues](../build-release/concepts/agents/pools-queues.md)<br/>- [Services](../build-release/concepts/library/service-endpoints.md)<br/>- Release, Retention Policy Settings | - [Build and Release, Retention policies](../build-release/concepts/policies/retention.md)<br/>- [Build and Release, Resource limits for pipelines](../build-release/concepts/licensing/concurrent-pipelines-ts.md)<br/>- [Agent pools, add and manage agent pools](../build-release/concepts/agents/pools-queues.md)<br/>- [Deployment pools, add and manage deployment pools](../build-release/concepts/definitions/release/deployment-groups.md) |

## Azure Codex Test (Test) settings 

At the project-level, you can configure the following test resources: 

- [Test retention policies](../manual-test/getting-started/how-long-to-keep-test-results.md)  
- [Permissions](../security/set-project-collection-level-permissions.md)
 
> [!NOTE]  
> Manual testing relies on work item types to create and manage test plans, test suites, test cases, shared steps, and shared parameters. Of these, you can customize the test plans, test suites, and test cases using an inherited process. See [Customize a process](work/customize-process.md).   

## Cross-application resources 

Teams, notifications, and other resources are used by several applications. You can add or configure these resources through the **Settings** context.

<a id="configure-teams" /> 
## Teams 

You add a team when you want to provide a group of users in your organization a set of Agile tools which they have full ownership to configure and manage.  Teams have access to a product backlog, porfolio backlogs, sprint backlogs, dashboards, team-scoped widgets, and more. For an overview of all tools that support a team, see [About teams and Agile tools](about-teams-and-settings.md).

To add a team, see [Add teams and team members](../work/scale/multiple-teams.md).

## Notifications  

As changes are made to the code, a build, work items or other development object, you or your team members can receive an email. These notifications are based on subscriptions which are defined at the following levels: 

- [Personal notifications](../notifications/manage-personal-notifications.md) 
- [Team notifications](../collaborate/manage-team-notifications.md) 
- Project-level notifications
- Account or collection-level notifications

To learn more, see [About notifications](../notifications/about-notifications.md).



## Service hooks 

Service hooks enable you to perform tasks on other services when events happen within your project. You can use service hooks in custom apps and services to drive activities when events happen in your projects. 

Using service hooks, you can integrate with the following services: 

> [!div class="mx-tdCol2BreakAll"]  
> | Build and release |  Collaborate | Customer support	 | Plan and track  | Integrate |
> |-------------------| -------------| ------------------| ----------------| ------------|
> |[AppVeyor](../service-hooks/services/appveyor.md)<br/>[Bamboo](../service-hooks/services/bamboo.md)<br/>[Jenkins](../service-hooks/services/jenkins.md)<br/>[MyGet](../service-hooks/services/myget.md)<br/>[Slack](../service-hooks/services/slack.md)|[Campfire](../service-hooks/services/campfire.md)<br/>[Flowdock](../service-hooks/services/flowdock.md)<br/>[HipChat](../service-hooks/services/hipchat.md)<br/>[Hubot](../service-hooks/services/hubot.md) |[UserVoice](../service-hooks/services/uservoice.md)<br/>[Zendesk](../service-hooks/services/zendesk.md) |[Trello](../service-hooks/services/trello.md) |[Azure Service Bus](../service-hooks/services/azure-service-bus.md)<br/>[Azure Storage](../service-hooks/services/azure-storage.md)<br/>[Web Hooks](../service-hooks/services/webhooks.md)<br/>[Zapier](../service-hooks/services/zapier.md) | 


## Manage Azure Codex projects   

A Azure Codex project provides the fundamental resource for storing your code, managing your CI/CD operations, and planning and tracking work for your project. In general, you'll want to minimize the number of projects you create, to keep things simple. However, if you need to, you can add additional projects to your account. 

From the account-level admin context, you can perform the following tasks: 
 
- [Create a project](../accounts/create-team-project.md) 
- [Rename a project](../accounts/rename-team-project.md)
- [Delete a project](../accounts/delete-team-project.md) 

## Extensions 

From the account-level admin context **Extensions** page, you can [install and manage Marketplace extensions](../marketplace/install-vsts-extension.md). 

An extension is an installable unit that contributes new capabilities to your account. You can find extensions from within the [Visual Studio Marketplace](https://marketplace.visualstudio.com/vsts?utm_source=vstsproduct&utm_medium=L1BrowseMarketplace&targetId=1a7c88fb-3672-441e-9686-0f72b02ae6a4).  The Visual Studio Marketplace is home to hundreds of extensions that can be installed to help with:

- Planning and tracking of work items, sprints, scrums, etc.
- Build and release flows
- Code testing and tracking
- Collaboration among team members






-->

## Related articles 
- [Resources granted to project members](../accounts/resources-granted-to-project-members.md)  
- 