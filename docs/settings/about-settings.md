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
<th width="18%">Area</th>
<th width="44%">Supported tasks</th>
<th width="36%">Notes</th>
</tr>
<tr>
<td>General</td>
<td><ul>
<li>[Set user preferences](../accounts/account-preferences.md)</li>
<li>[View permissions](../security/view-permissions.md)</li>
<li>[Enable preview features](../collaborate/preview-features.md)</li>
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
<li>[Manage personal notifications](../notifications/manage-personal-notifications.md)</li>
</ul></td>
<td>To learn more about how notifications are managed, see [About notifications](../notifications/about-notifications.md).</li>
</ul></td>
</tr>
</tbody>
</table>
 

## Team administrator role and managing teams

Team administrators are tasked with configuring team resources which mostly correspond to Agile tools and dashboards.  


<table>
<tbody valign="top">
<tr>
<th width="18%">Area</th>
<th width="44%">Supported tasks</th>
<th width="36%">Notes</th>
</tr>
<tr>
<td>General</td>
<td><ul>
<li>[Add user accounts to a team](../accounts/account-preferences.md)</td>
<td>Members of a team are included within the team group which can be used in queries and **@mentions** in pull requests and work item discussions.</td>
</tr>
<tr>
<td>Azure Codex Agile<br/>(Work tracking)</td>
<td><ul>
<li>[Configure team default area and iteration paths](../work/scale/set-team-defaults.md)</li>
<li>[Select iteration paths that they'll use](../work/scale/set-team-defaults.md)</li>
<li>Configure Kanban boards: [Columns](../work/kanban/add-columns.md), [Swimlanes](../work/kanban/expedite-work.md), [Cards](../work/customize/customize-cards.md), [WIP limits](../work/kanban/wip-limits.md)</li>
<li>[Configure additional team settings](../work/scale/manage-team-assets.md)</li>
<li>[Define work item templates](../work/backlogs/work-item-template.md)</li>
</ul></td>
<td>To configure team resources, you must be added as a [team administrator for the specific team](../work/scale/add-team-administrator.md).  </td>
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
<td>TBD </td>
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

## Project administrator role 

Members of the [Project Administrators group](../security/set-project-collection-level-permissions.md) are tasked with configuring resources for a project and managing permissions at the project-level.  

<table>
<tbody valign="top">
<tr>
<th width="18%">Area</th>
<th width="44%">Supported tasks</th>
<th width="36%">Notes</th>
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
<td>Azure Codex Agile<br/>(Work tracking)</td>
<td><ul>
<li>[Define area paths](set-area-paths.md)</li>
<li>[Define iteration paths or sprints](set-iteration-paths-sprints.md)</li>
</ul></td>
<td>Area and iteration paths set at the project level are then used to set team defaults. </td>
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
<td>Permissions can be given at [project level](../security/set-project-collection-level-permissions.md) and at [area path level](../security/set-permissions-access-work-tracking.md#create-child-nodes-modify-work-items-under-an-area-path).</td>
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
<td>Notifications at the project level are managed in much the same way as they are at the [team level](../collaborate/manage-team-notifications.md).</td>
</tr>
<tr>
<td>Ecosystem</td>
<td><ul>
<li>[Configure service hooks to integrate with other services](../service-hooks/index.md)</li>
</ul></td>
<td>With service hooks, you can automate a task on other services, such as Campfire, Flowdock, HipChat, and more, when events happen in your Azure Codex project.</td>
</tr>
</tbody>
</table>


<!---

> [!div class="mx-tdCol2BreakAll"]  
> |  Area  | Supported tasks | Notes |
> |---------|---------|---------|  
> | General |- [Add user accounts to a team project](../accounts/account-preferences.md)<br/>- [Add another team](../work/scale/multiple-teams.md)| TBD   | 
> | Azure Codex Agile<br/>(Work tracking) |- [Define area paths](set-area-paths.md)<br/>- [Define iteration paths or sprints](set-iteration-paths-sprints.md) | Area and iteration paths set at the project level are then used to set team defaults.  |
> | Azure Codex Repos<br/>(Code management  |- [Create additional Git repos](../git/tutorial/creatingrepo.md)<br/>- [Manage repository permissions](../security/set-git-tfvc-repository-permissions.md)  | TBD |
> | Azure Codex Pipelines<br/>(Build & Release management)|- [Add and manage Agent queues](../build-release/concepts/agents/pools-queues.md)<br/>- [Add and manage service endpoints](../build-release/concepts/library/service-endpoints.md)<br/>- [Set retention policies](../build-release/concepts/policies/retention.md)  | TBD |
> | Azure Codex Test<br/>(Test management)| - [Set test retention policies](../manual-test/getting-started/how-long-to-keep-test-results.md)<br/>- Manage test-related permissions | Permissions can be given at [project level](../security/set-project-collection-level-permissions.md) and at [area path level](../security/set-permissions-access-work-tracking.md#create-child-nodes-modify-work-items-under-an-area-path).  | 
> | Notifications |- Manage project-level notifications |  Notifications at the project level are managed in much the same way as they are at the [team level](../collaborate/manage-team-notifications.md). |
> | Ecosystem |- [Configure service hooks to integrate with other services](../service-hooks/index.md) | With service hooks, you can automate a task on other services, such as Campfire, Flowdock, HipChat, and more, when events happen in your Azure Codex project. |

--> 

## Project collection administrator role 

Members of the [Project Collection Administrators group](../security/set-project-collection-level-permissions.md) are tasked with configuring resources for all Azure Codex projects defined for an account or organization. They also can perform all tasks to manage projects and manage permissions at the collection-level.  

<td><ul>
<li>[Add and manage Agent queues](../build-release/concepts/agents/pools-queues.md)</li>
<li>[Add and manage service endpoints](../build-release/concepts/library/service-endpoints.md)</li>
<li>[Set retention policies](../build-release/concepts/policies/retention.md)</li>
</ul></td>


<table>
<tbody valign="top">
<tr>
<th width="18%">Area</th>
<th width="44%">Supported tasks</th>
<th width="36%">Notes</th>
</tr>
<tr>
<td>General</td>
<td><ul>
<li>Add and manage projects: [Create a project](../accounts/create-team-project.md), [Rename](../accounts/rename-team-project.md), [Delete](../accounts/delete-team-project.md)</li>
<li>Manage account settings</li>
<li>Manage billing</li>
</ul></td>
<td>TBD</td>
</tr>
<tr>
<td>Security</td>
<td><ul>
<li>Add administrators</li>
<li>Add users or remove users to an organization</li>
<li>Assign access levels and extensions </li>
</ul></td>
<td>TBD</td>
</tr>
<tr>
<td>Azure Codex Agile<br/>(Work tracking)</td>
<td><ul>
<li>[Customize a project](./work/customize-process.md)</li>
<li>[Add and manage processes](./work/manage-process.md </li>
</ul></td>
<td>To customize the Agile tools and work tracking artifacts, you create and customize an inherited process and then update the project to use that process. To learn more, see [About process customization and inherited processes ](./work/inheritance-process-model.md). </td>
</tr>
<tr>
<td>Azure Codex Pipelines<br/>(Build & Release management)</td>
<td><ul>
<li>[Set retention policies](../build-release/concepts/policies/retention.md)</li>
<li>[Set resource limits for pipelines](../build-release/concepts/licensing/concurrent-pipelines-ts.md)</li>
<li>[Add and manage agent pools](../build-release/concepts/agents/pools-queues.md)</li>
<li>[Add and manage deployment pools](../build-release/concepts/definitions/release/deployment-groups.md)</li>
</ul></td>
<td> TBD </td>
</tr>
<tr>
<td> Notifications </td>
<td><ul>
<li>Manage collection-level notifications </li>
</ul></td>
<td>Notifications at the project level are managed in much the same way as they are at the [team level](../collaborate/manage-team-notifications.md).</td>
</tr>
<tr>
<td>Extensions</td>
<td><ul>
<li>[Install and manage Marketplace extensions](../marketplace/install-vsts-extension.md)</li>
</ul></td>
<td>[Marketplace extensions](https://marketplace.visualstudio.com/vsts) provide additional features and capabilities to your Azure Codex project.</td>
</tr>
</tbody>
</table>


<!---
> [!div class="mx-tdCol2BreakAll"]  
> |  Area  | Supported tasks | Notes |
> |---------|---------|---------|  
> | General |- Add and manage projects: [Create a project](../accounts/create-team-project.md), [Rename](../accounts/rename-team-project.md), [Delete](../accounts/delete-team-project.md)<br/>- Manage account settings<br/>- Manage billing | TBD   | 
> | Security | - Add administrators<br/>- Add users or remove users to an organization<br/>-  
Assign access levels and extensions  | TBD |
> | Azure Codex Agile<br/>(Work tracking) |- [Customize a project](./work/customize-process.md)<br/>- [Add and manage processes](./work/manage-process.md) | To customize the Agile tools and work tracking artifacts, you create and customize an inherited process and then update the project to use that process. To learn more, see [About process customization and inherited processes ](./work/inheritance-process-model.md).   |
> | Azure Codex Repos<br/>(Code management  |- [Create additional Git repos](../git/tutorial/creatingrepo.md)<br/>- [Manage repository permissions](../security/set-git-tfvc-repository-permissions.md)  | TBD |
> | Azure Codex Pipelines<br/>(Build & Release management)|- [Set retention policies](../build-release/concepts/policies/retention.md)<br/>- [Set resource limits for pipelines](../build-release/concepts/licensing/concurrent-pipelines-ts.md)<br/>- [Add and manage agent pools](../build-release/concepts/agents/pools-queues.md)<br/>- [Add and manage deployment pools](../build-release/concepts/definitions/release/deployment-groups.md)<br/> | TBD |
> | Notifications |- Manage collection-level notifications |  Notifications at the project level are managed in much the same way as they are at the [team level](../collaborate/manage-team-notifications.md). |
> | Extension |- [Install and manage Marketplace extensions](../marketplace/install-vsts-extension.md) | Extensions provide additional features and capabilities to your Azure Codex project. |


-->

<!---

## Azure Codex Agile (Work tracking) settings

Many work tracking/Agile tools provide teams the autonomy they need to configure and manage their work independent of other teams. When you add a team, you also configure a product backlog, Kanban board, and dashboard for the teams. To learn more, see [About teams and Agile tools](about-teams-and-settings.md). 

You configure work tracking settings at one of the following three levels. 

> [!div class="mx-tdCol2BreakAll"]  
> |  Team  | Project | Organization | 
> |------|---------|---------|
|- [Backlog levels](../work/customize/select-backlog-navigation-levels.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json)<br/>- [Show bugs on backlogs & boards](../work/customize/show-bugs-on-backlog.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json<br/>- [Set working days](../work/customize/set-working-days.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json)<br/>- [Default areas & iterations](../work/scale/set-team-defaults.md)<br/>- [Work item templates](../work/backlogs/work-item-template.md?toc=/vsts/settings/toc.json&bc=/vsts/settings/breadcrumb/toc.json) |- [Area paths](../work/customize/set-area-paths.md)<br/>- [Iteration paths aka sprints](../work/customize/set-iteration-paths-sprints.md)| - [Customize a project](./work/customize-process.md)<br/>- [Create and manage a process](./work/manage-process.md)<br/>- [Add and manage fields](./work/customize-process-field.md)<br/>- [Add and manage work item types](./work/customize-process-wit.md)<br/>- [Customize a web form](./work/customize-process-form.md)<br/>- [Customize a workflow](./work/customize-process-workflow.md)<br/>- [Add a custom rule](./work/custom-rules.md)<br/>- [Add a custom control](./work/custom-controls-process.md)<br/>- [Customize backlogs and boards](./work/customize-process-backlogs-boards.md) |

To configure additional product backlogs, Kanban boards, and dashboards, you [configure a team](#configure-team).   

To customize the workflow, work item form, add fields or rules, or make other changes to the work tracking experience, you customize a process. For an overview of what you can customize, see [About process customization and inherited processes](work/inheritance-process-model.md). 
 
To change permissions at the project-level, many of which are work tracking related, see [Set permissions at the project-level or project collection-level](../security/set-project-collection-level-permissions.md)
 

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


## Additional organizational-level settings

In addition to the app-specific resources that you can configure, you can also manage your account, users, extensions, and organizational-level permissions. 

### Organizational-level settings

From the account-level **Settings** page, you can change the time zone for your account and perform the following tasks: 
- [Change account owner](../accounts/change-account-ownership-vs.md) 
- [Rename your account](../accounts/rename-vsts-account.md) 
- [Delete your account](../accounts/delete-your-vsts-account.md) 
- [Restore (a deleted) account](../accounts/recover-your-vsts-account.md)
- [Find your account region](../accounts/change-account-location.md) 
- [Connect your account to Azure Active Directory](../accounts/connect-account-to-aad.md) 
- [Set up Azure billin](../billing/set-up-billing-for-your-account-vs.md)


### Users 
From the account-level **Users** page, you can export the set of users and their access levels. You can also perform the following tasks: 
- [Add users to your project](../accounts/add-account-users-from-user-hub.md)
- [Remove users from your account](../accounts/delete-account-users.md)
- [Assign access levels and extensions to users by group membership](../accounts/assign-access-levels-and-extensions-by-group-membership.md)


### Account-level permissions or Security  

From a Security page or dialog, you can set permissions for a user or group. Permissions are managed at the object, project, and account level. To learn more, see [About permissions and groups](../security/about-permissions.md).

To manage collection-level permissions, see [Add administrators, set permissions at the project-level or project collection-level](../security/set-project-collection-level-permissions.md?toc=/vsts/security/toc.json&bc=/vsts/security/breadcrumb/toc.json). 




You must be a member of the listed administrator group or role to configure resources at the levels indicated. To learn more about security groups and roles, see [About permissions and groups](../security/about-permissions.md) and [About security roles](../security/about-security-role.md). 


## Team level  

To configure team resources, you must be a member of the [team administrator role](../work/scale/add-team-administrator.md) for the team, or a member of the Project Administrators or Project Collection Administrators groups.  

- [Overview: Add team members](../work/scale/multiple-teams.md) 
- [Add team admins](../work/scale/add-team-administrator.md)
- [Select backlog levels](../work/customize/select-backlog-navigation-levels.md) 
- [Set working days](../work/scale/capacity-planning.md) 
- [Working with bugs](../work/customize/show-bugs-on-backlog.md)
- [Work/Iterations & Areas (team defaults)](../work/scale/set-team-defaults.md)
- [Work/Templates](../work/backlogs/work-item-template.md)<br/>- [Security (manage team-level permissions)](../work/scale/team-administrator-permissions.md)
- [Notifications](../collaborate/manage-team-notifications.md)

For a complete overview of all team assets that you can configure, see  [Manage team assets](../work/scale/manage-team-assets.md) 


-->