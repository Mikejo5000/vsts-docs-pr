---
title: Account and project scope queries
description: How to query the OData Analytics service on account and project level  
ms.prod: vs-devops-alm
ms.technology: vs-devops-reporting
ms.assetid: 0ABC2F7B-AFA5-465F-8DFE-4779D90452CD  
ms.manager: douge
ms.author: kokosins
ms.date: 11/15/2017
---

#Account and project scope queries


The Analytics Service supports querying on an account level and on a project level.


Base URL for account level queries:
```
https://{account}.analytics.visualstudio.com/_odata/v1.0
```

Base URL for project level queries:
 ```
https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0
```
>[!NOTE]
>If you don't have access to all projects in an account, apply a project filter to your query. When pulling data into client tools such as
>Power BI Desktop or Excel, use the project path form of the URL to ensure your data is constrained by a project, unless you need to report on more than one project.

For example, the following project-scoped query will return the count of work items for a specific project:  

```
https://{account}.analytics.visualstudio.com/ProjectA/_odata/v1.0/WorkItems/$count
```

Likewise, this query string will return the areas for a specific project:

```
https://{account}.analytics.visualstudio.com/ProjectA/_odata/v1.0/Areas
```

This is equivalent to the following filter on a account-scoped query:

```
https://{account}.analytics.visualstudio.com/_odata/v1.0/Areas?$filter=Project/ProjectName eq 'ProjectA'
```

When using a project-scoped query with an ```$expand``` you are not required to provide additional filters.

For example, the following project scoped filter:

```
https://{account}.analytics.visualstudio.com/ProjectA/_odata/v1.0/WorkItems?$expand=Parent
```

would be filtered automatically to enforce security:

```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$filter=ProjectName eq 'ProjectA'&$expand=Parent($filter=ProjectName eq 'ProjectA')
```


When using a account-scoped query with an ```$expand``` you must provide an additional filter.

For example, the following account-scoped query, which uses an ```$expand``` to retrieve the children of all work items:
	
```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$expand=Children&$filter=Project/ProjectName eq 'ProjectA'
```

requires an additional filter to verify the children are limited to the specified project:
	
```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$expand=Children($filter=Project/ProjectName eq 'ProjectA')&$filter=Project/ProjectName eq 'ProjectA'
```

This query, which uses an ```$expand``` to retrieve the parent of all work items:

```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$expand=Parent&$filter=Project/ProjectName eq 'ProjectA'
```

Requires an additional filter to verify the parent is limited to the specified project:

```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$expand=Parent($filter=Project/ProjectName eq 'ProjectA')&$filter=Project/ProjectName eq 'ProjectA'
```

Without the additional filter, the request will fail if the parent of any work item references work items in a project that you do not have read access to.


The Analytics Service has a few additional restrictions on query syntax related to project level security.

The ```any``` or ```all``` filters apply to the base Entity on an ```$expand```.  For filters based on a Project we explicitly ignore the filter when using an ```$expand```:
	
```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$expand=Children&$filter=ProjectName eq 'ProjectA' and Children/any(r: r/ProjectName eq 'ProjectA')
```

Using ```$level``` is only supported if you have access to all projects in the collection or when using a project scoped query:
	
```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$expand=Children($levels=2;$filter=ProjectName eq 'ProjectA')
```

Analytics does not understand or support any cross level reference with Projects. As an example, this query is referencing the root work item’s ProjectName using $it alias which is unsupported:

```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$expand=Links($expand=TargetWorkItem;$filter=TargetWorkItem/Project/ProjectName eq $it/Project/ProjectName)
```

