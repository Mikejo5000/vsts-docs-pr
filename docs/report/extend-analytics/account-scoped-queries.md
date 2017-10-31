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

#Account and project-scopes queries

**VSTS**  

[!INCLUDE [temp](../_shared/analytics-preview.md)]

Project-scope queries help answer questions about a single project. And at the same time, account-scope queries allow you to answer questions which cross project boundaries. However, account scoped queries require broader user permissions or careful scoping scoping restrictions to ensure the query is not blocked with permissions for projects a user does not have access to.

Base URL for account level queries:
```
https://{account}.analytics.visualstudio.com/_odata/v1.0
```

Base URL for project level queries:
 ```
https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0
```

The following project-scoped query will return the count of work items for a specific project:  

>[!NOTE]
>If you don’t have access to all projects in an account, it is recommended to apply a project filter to all of your queries. When pulling data into client tools such as Power BI Desktop or Excel, using the project path syntax is the best way to ensure that all your data is constrained by the given project. It is only recommended to use the account-scoped queries when you need to report on more than one project.


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
###  Security related restriction

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

requires an additional filter to verify the parent is limited to the specified project:

```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$expand=Parent($filter=Project/ProjectName eq 'ProjectA')&$filter=Project/ProjectName eq 'ProjectA'
```

Without the additional filter, the request will fail if the parent of any work item references work items in a project that you do not have read access to.


The Analytics Service has a few additional restrictions on query syntax related to project level security.

The ```any``` or ```all``` filters apply to the base Entity on an ```$expand```.  For filters based on a Project we explicitly ignore the filter when using an ```$expand```:

For example, following query:
```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$expand=Children($filter=Project/ProjectName eq 'ProjectA')&$filter=ProjectName eq 'ProjectA'
```
will in interpreted as:
```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$expand=Children&$filter=ProjectName eq 'ProjectA'
```
at will fail when you don't have access to all projects.
	
To workaround that restriction you need extra expression inf the ```$filter```:
```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$expand=Children&$filter=ProjectName eq 'ProjectA' and Children/any(r: r/ProjectName eq 'ProjectA')
```

Using ```$level``` is only supported if you have access to all projects in the collection or when using a project scoped query:
	
```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$expand=Children($levels=2;$filter=ProjectName eq 'ProjectA')
```

Analytics does not support any cross level reference for projects using $it alias. As an example, this query is referencing the root work item’s ProjectName using $it alias which is unsupported:

```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$expand=Links($expand=TargetWorkItem;$filter=TargetWorkItem/Project/ProjectName eq $it/Project/ProjectName)
```

