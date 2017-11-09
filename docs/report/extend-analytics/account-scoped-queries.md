---
title: Account and project scope queries
description: How to query the OData Analytics service on account and project level  
ms.prod: vs-devops-alm
ms.technology: vs-devops-reporting
ms.assetid: 0ABC2F7B-AFA5-465F-8DFE-4779D90452CD  
ms.manager: trevorc
ms.author: kokosins
ms.date: 11/15/2017
---

#Account and project-scopes queries

**VSTS**  

[!INCLUDE [temp](../_shared/analytics-preview.md)]

Project-scope queries help answer questions about a single project. And at the same time, account-scope queries allow you to answer questions which cross project boundaries. However, account scoped queries require broader user permissions or careful scoping restrictions to ensure that the query isn’t blocked due to a lack of project permissions.

Base URL for account level queries:
```
https://{account}.analytics.visualstudio.com/_odata/v1.0
```
## Project-scoped queries
Base URL for project level queries:
 ```odata
https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0
```

The following project-scoped query will return the count of work items for a specific project:  

>[!NOTE]
>If you don’t have access to all projects in an account, it is recommended to apply a project filter to all of your queries. When pulling data into client tools such as Power BI Desktop or Excel, using the project path syntax is the best way to ensure that all your data is constrained by the given project. We recommend you use account-scoped queries only when you need to report on two or more projects.


```odata
https://{account}.analytics.visualstudio.com/ProjectA/_odata/v1.0/WorkItems/$count
```

Likewise, this query string will return the areas for a specific project:

```odata
https://{account}.analytics.visualstudio.com/ProjectA/_odata/v1.0/Areas
```

This is equivalent to the following filter on an account-scoped query:

```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/Areas?
  $filter=Project/ProjectName eq 'ProjectA'
```

When using a project-scoped query with an ```$expand``` option you are not required to provide additional filters.

For example, the following project-scoped filter:

``` odata
https://{account}.analytics.visualstudio.com/ProjectA/_odata/v1.0/WorkItems?
  $expand=Parent
```

is filtered automatically to enforce security:

```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=ProjectName eq 'ProjectA'
  &$expand=Parent($filter=ProjectName eq 'ProjectA')
```
##  Account-scoped queries and security related restrictions

When using an account-scoped query with an ```$expand``` option you must provide an additional filter.

For example, the following account-scoped query, which uses an ```$expand``` to retrieve the children of all work items:
	
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=Project/ProjectName eq 'ProjectA'
  &$expand=Children
```

requires an additional filter to verify the children are limited to the specified project:
	
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=Project/ProjectName eq 'ProjectA'
  &$expand=Children($filter=Project/ProjectName eq 'ProjectA')
```

This query, which uses an ```$expand``` option to retrieve the parent of all work items:

```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=Project/ProjectName eq 'ProjectA'
  &$expand=Parent

```

requires an additional filter to verify the parent is limited to the specified project:

```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=Project/ProjectName eq 'ProjectA'
  &$expand=Parent($filter=Project/ProjectName eq 'ProjectA')
```

Without the additional filter, the request will fail if the parent of any work item references work items in a project that you do not have read access to.


The Analytics Service has a few additional restrictions on query syntax related to project level security.

The ```any``` or ```all``` filters apply to the base Entity on an ```$expand```.  For filters based on a Project we explicitly ignore the filter when using an ```$expand```:

For example, the following query:
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=ProjectName eq 'ProjectA'
  &$expand=Children($filter=Project/ProjectName eq 'ProjectA')
```
is interpreted as:
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=ProjectName eq 'ProjectA'
  &$expand=Children
```
and will fail if you don’t have access to all projects.
	
To workaround the restriction, you need to add an extra expression in the ```$filter```:
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=ProjectName eq 'ProjectA' and Children/any(r: r/ProjectName eq 'ProjectA')
  &$expand=Children
```

Using ```$level``` is only supported if you have access to all projects in the collection or when using a project-scoped query:
	
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $expand=Children($levels=2;$filter=ProjectName eq 'ProjectA')
```

Analytics does not support any cross-level reference for projects using $it alias. As an example, the following query references the root work item’s ProjectName using $it alias, which isn’t supported:

```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $expand=Links(
    $expand=TargetWorkItem;
    $filter=TargetWorkItem/Project/ProjectName eq $it/Project/ProjectName)
```

