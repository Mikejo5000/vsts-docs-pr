---
title: Analytics basic queries | VSTS  
description: Provides general queries for use with the Analytics service for VSTS (SEO; work item history, work items in a given iteration, work item in a given area, work items per project, work items per iteration, work items per tag, work items per team, cumulative flow diagram)
ms.prod: vs-devops-alm
ms.technology: vs-devops-reporting
ms.assetid: 1320852A-5C62-4954-9E9D-508D670777A4
ms.manager: douge
ms.author: kaelli
ms.date: 08/11/2016
---

#Analytics service basic queries  

**VSTS**  

[!INCLUDE [temp](../_shared/analytics-preview.md)]

This topic provides a set of general queries that demonstrate various querying capabilities of the
analytics service and which also provides common queries which solve everyday needs. Most of these can be 
adapted for different needs. 

**Retrieve the history of a work item**

```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItemRevisions?$filter=WorkItemId eq {Id}
```

**Retrieve all work items in a given iteration**

```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$filter=Iteration/IterationPath eq '{iteration path}'
```

**Retrieve all work items in a given area**

```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$filter=Area/AreaPath eq '{area path}'
```

**Get the count of work items in each project**
```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$apply=groupby((Project/ProjectName), aggregate($count as Count))
```

**Retrieve all work items for a given iteration which fall between the first day of the iteration and the last day of the iteration**

Here your query is constrained by data 
contained within the VSTS data. 

```
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$filter=Iteration/IterationPath eq '{iteration path}' and ChangedDate ge Iteration/StartDate and ChangedDate le Iteration/EndDate
```

**Retrieve all work items with a specific tag**

Note that the **any** operator is used here because there are a collection of tags that can be associated with a work item.
From a usage perspective, the format is: **{Navigation Property}/any(d:d/{Field Name} {operator} {expression})**. Any item not surrounded by curly brackets ({}) is a literal. There are some variations on this (for example, you don't have to use "d" as used in the expression above)
but following this format keeps it simple.

```
https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/WorkItems?$filter=Tags/any(d:d/TagName eq '{tag name}')
```

**Retrieve all work items for a specific team**

```
https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/WorkItems?$filter=Teams/any(d:d/TeamName eq '{team name}')&$select=WorkItemId,Title,State
```
##Related notes 

- [WIT analytics](wit-analytics.md)  
- [Aggregate data](aggregated-data-analytics.md)
- [Overview of the analytics service](overview-analytics-service.md)
