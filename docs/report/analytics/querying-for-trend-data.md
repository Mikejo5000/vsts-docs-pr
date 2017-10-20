---
title: Query for trend data | VSTS  
description: How to query the Analytics service for trend data and consume it in a client tool when working from Visual Studio Team Services (VSTS) 
ms.prod: vs-devops-alm
ms.technology: vs-devops-reporting
ms.assetid: FEF88D72-32D7-4DE8-B11E-BCB1A491C3FC
ms.manager: douge
ms.author: kaelli
ms.date: 08/04/2017
---

# Query for trend data

**VSTS**  

[!INCLUDE [temp](../_shared/analytics-preview.md)]

Examining trends in data and making period-over-period comparisons are two of the most interesting aspects of data analysis. The Analytics service supports this capability.

Trend data is captured in the WorkItemSnapshot and WorkItemBoardSnapshot entities. They are constructed such that every work item, from the day it was created until today, exists for each day. This means that for an account with only one work item that was created a year ago, there are 365 rows in this entity.  

For any project of size, this entity will be far too large to load into a client tool.  

What is the solution? [Aggregation Extensions](../aggregated-data-analytics.md). 

Using the OData Aggregation Extensions, you can return aggregated data from VSTS that is conducive to reporting. For example you could show bug trend for the month of March. Bug trends are a common and critical part of managing any project so you can put this to good use immediately.

See the topic [Aggregate data](aggregated-data-analytics.md) for more detailed information on
constructing aggregation queries.

##Construct the basic query    
There are some basic requirements you need to effectively query the WorkItemSnapshot table:  
* The data needs to be filtered by date.
* The aggregation should group by, at the very least, date.

With this in mind, the query to create a bug trend report looks like the following: 

```
https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/WorkItemSnapshot?$apply=filter(Date/Date ge 2016-03-01 and Date/Date le 2016-03-31 and WorkItemTyp eq 'Bug')/groupby((Date/Date,State), aggregate(Count with sum as Count))&$orderby=Date/Date
```

This query will produce at most ```31 * (number of bug states)```. The default bug has three states 
(Active, Resolved and Closed) which means at most this query will return 93 rows no matter 
how many thousands of records actually exist. This provides a much more compact form of returning data and it also loads faster into client tools.  

Before walking you through how to use this in a client tool, let's look at a variation on this example. You want to see the bug trend for an iteration or a release which starts with one iteration and ends with another.  

To construct that query, do the following:  

```
https://{account}.analytics.visualstudio.com/DefaultCollection/{project}/_odata/v1.0/WorkItemSnapshot?$apply=filter(Iteration/IterationName eq 'Sprint 99')/filter(Date/Date ge Iteration/StartDate and Date/Date le Iteration/EndDate and WorkItemType eq 'Bug')/groupby((Date/Date,State), aggregate(Count with sum as Count))&$orderby=Date/Date
```

In this query, there are two key differences. We added a filter clause to filter the data to a specific iteration and the dates are now being compared to the iteration start and end dates versus a hard coded date.  

>[!NOTE]  
>Using Power Query you can craft the query such that it provides a rolling chart using a formal, such as, todays date minus 30 days for a rolling 30 day chart.
