---
title: About teams | Team Services & TFS 
description: Understand how to scale your system with teams-Visual Studio Team Services and Team Foundation Server   
ms.technology: vs-devops-agile-wit
ms.prod: vs-devops-alm
ms.assetid: E4DBCBA5-33B5-4A8F-979A-793BE6FD63DF
ms.manager: douge
ms.author: kaelli
ms.date: 06/22/2017
---

# About teams and team tools 

Adding a team is the #1 way in which Agile tools supports a growing organization. Once your team grows beyond its optimum size&mdash;typically anywhere from 6 to 9 members&mdash;you might consider moving from a one team structure to a two team structure. For enterprises adopting Agile tools, setting up a hierarchical team structure provides several advantages to portfolio and program managers to track progress across several teams.  

Each team you create gets access to a suite of Agile tools and team assets. These tools provide teams the ability to work autonomously and collaborate with other teams across the enterprise. 

![Agile tool team assets](_img/agile-tools-team-assets.png) 


To learn more about each tool, see the following topics: 

<div style="float:left;width:200px;margin:3px;font-size:90%">
<p style="font-weight:bold;padding-bottom:0px;text-align:center;">Plan and track</p>
<ul style="padding-left:30px">
 <li style="margin-bottom:2px">[Product backlog](../backlogs/create-your-backlog.md)</li>
 <li style="margin-bottom:2px">[Kanban board](../kanban/kanban-basics.md)</li>
 <li style="margin-bottom:2px">[Portfolio backlogs](../backlogs/define-features-epics.md)</li>
 <li style="margin-bottom:2px">[Sprint backlogs](../scrum/sprint-planning.md)</li>
 <li style="margin-bottom:2px">[Sprint task boards](../scrum/task-board.md)</li>
 <li style="margin-bottom:2px">[Capacity planning](capacity-planning.md)</li>
 <li style="margin-bottom:2px">[Forecasting](../scrum/velocity-and-forecasting.md)</li>
</ul>
</div>


<div style="float:left;width:200px;margin:3px;font-size:90%">
<p style="font-weight:bold;padding-bottom:0px;text-align:center;">Collaborate</p>
<ul style="padding-left:30px">
 <li style="margin-bottom:2px">[Team alerts](../track/alerts-and-notifications.md)</li>
 <li style="margin-bottom:2px">[Team favorites](manage-team-assets.md#team-favorites)</li>
 <li style="margin-bottom:2px">[Team group](manage-team-assets.md#team-group)</li>
 <li style="margin-bottom:2px">[Team rooms](../../collaborate/collaborate-in-a-team-room.md)</li>

</ul>
</div>

<div style="float:left;width:200px;margin:3px;font-size:90%">
<p style="font-weight:bold;padding-bottom:0px;text-align:center;">Monitor and learn</p>
<ul style="padding-left:30px">
<li style="margin-bottom:2px">[Velocity chart](../scrum/velocity-and-forecasting.md)</li>
 <li style="margin-bottom:2px">[Cumulative flow chart](../../report/guidance/cumulative-flow.md)</li>
 <li style="margin-bottom:2px">[Capacity bars per sprint](capacity-planning.md)</li>
 <li style="margin-bottom:2px">[Sprint burndown charts](../scrum/sprint-burndown.md)</li>
 <li style="margin-bottom:2px">[Team dashboards](../../report/dashboards.md) </li> 
</ul>
</div>


<div style="clear:left;font-size:100%">
</div>


<a id="collection-project-team-structure">  </a>
### Collection-project-team structure
When you connect to Team Services or an on-premises TFS, you connect to an account or team project collection. Within that collection, one or more team projects may be defined. At a minimum, at least one team project must be created in order to use the system.

When you create your team project, a team of the same name is automatically created. For small teams, this is sufficient.  

However, for enterprise-level organizations, it may be necessary to scale up, to create additional teams and/or team projects. These can be created within the single account or collection.

<table width="100%">
<tbody valign="top">
<tr>
<td width="40%">
**Single team project, team defined within an account/collection**  
![Single collection-project-team conceptual image](../../connect/_img/web-portal-account-project-team-concept.png)  
</td>

<td width="60%">
**Multiple team projects and teams defined within an account/collection**   
![Scaled collection-project-team conceptual image](../../connect/_img/web-portal-account-project-team-scale-concept.png)  

</td>
</tr>
</tbody>
</table>

The collection-project-team structure provides teams a high-level of autonomy to configure their tools in ways that work for them. It also supports administrative tasks to occur at the appropriate level.

To learn more about adding teams and the features that support team autonomy, see [Multiple teams](multiple-teams.md) and [Manage team assets](manage-team-assets.md).

 
## Related notes
 
- [Configure team settings, add team administrators](manage-team-assets.md)  
- [Visibility across teams](visibility-across-teams.md)  
- [Review team plans](review-team-plans.md)    
- [Track work when contributing to several teams](capacity-planning.md)
- [Scaled Agile Framework](scaled-agile-framework.md)   
- [Practices that scale](practices-that-scale.md) 
- [Restrict access to select features and functions](../../setup-admin/restrict-access-tfs.md)   



<a id="team-group"> </a>
### Team groups 

You can use this group to filter queries. The name of team groups follows the pattern [Team Project Name]\Team Name. For example, the following query finds work assigned to members of the [Fabrikam Fiber]\Email team group.

<img src="_img/query-in-group-email-team-work-in-progress.png" alt="Web portal, Queries page, Query that uses In Group operator and team group name" style="border: 1px solid #CCCCCC;" /> 

### Work on more than one team

Can a user account belong to more than one team?  

Yes. When you add user accounts to a team project, you can add them as members of the team project, or you can add them to one or more teams added to the team project. If you work on two or more Scrum teams, you'll want to make sure you, [specify your sprint capacity for each team you work on](capacity-planning.md). 

