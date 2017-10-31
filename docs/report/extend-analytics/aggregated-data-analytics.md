---
title: Aggregate data using the OData Analytics Service for VSTS  
description: How to aggregate data with the Analytics Service (SEO; aggregation extension in odata, filtering of aggregated results)
ms.prod: vs-devops-alm
ms.technology: vs-devops-reporting
ms.assetid: 8D81FEFD-F432-4E10-A415-9167B5FE9A57 
ms.manager: douge
ms.author: kaelli
ms.date: 10/31/2017
---

# Aggregate data using the Analytics service   

**VSTS**  

[!INCLUDE [temp](../_shared/analytics-preview.md)]

You can aggregate your VSTS data using the OData Analytics service and the Aggregation Extension.

##What is the Aggregation Extension for OData?

Analytics relies on OData to author queries over your VSTS data. Aggregations in OData are achieved using an extension that introduces the ```$apply``` keyword. We have some examples of how to use this keyword below. Learn more about the extension at [OData Extension for Data Aggregation](http://docs.oasis-open.org/odata/odata-data-aggregation-ext/v4.0/cs01/odata-data-aggregation-ext-v4.0-cs01.html).

There are two ways to aggregate data. The simple approach without using aggregation extension provides just the count of data. The more advanced approach performs aggregations available via the aggregation extensions. 

Use the following basic root URL as a prefix for all the examples provided in this topic.

```
https://{account}.analytics.visualstudio.com/_odata/v1.0
``` 


Use the above URL as a prefix for all the examples.   


##Simple count aggregations

First, let's look at how to do counts without the aggregation extensions.

Basic counting is done by adding the ```$count``` query option to the end of the URL. For example, to find out how many work items are in the system you can
issue the following query:

    /WorkItems/$count

For comparison, using data aggregations you enter this query:

    /WorkItems?$apply=aggregate($count as Count)

For simple counts, the non-aggregation approach has a simpler syntax.  
 

>[!NOTE]  
>There is one other difference in these approaches: Using ```$count``` returns a single number. Using aggregation extensions returns a formatted JSON.  
  

You can also filter what you want to count. For example, if you want to know how many work items are in the "In Progress" state, specify this query:

    /WorkItems/$count?$filter=State eq 'In Progress'

For comparison, using data aggregations you enter this query:

    /WorkItems?$apply=filter(State eq 'In Progress')/aggregate($count as Count)


## Aggregate data using aggregation extension

Now that you've seen how to do simple counts, let's review how to trigger aggregations using the ```$apply``` token where the basic format at the end of the URL is as follows:


    /{entityName}?$apply=aggregate({columnToAggregate} with {aggregationType} as {newColumnName})

{entityName} is the entity that needs to be queried for. {columnToAggregate} is the aggregation column. {aggregationType} will specify the type of aggregation used and {newColumnName} specifies the name of the column having values after aggregation.

### Aggregated data examples 

Using the ```apply``` extension, you can obtain counts, sums, and additional information when you query your VSTS data. 

**Return the count of work items:**

    /WorkItems?$apply=aggregate($count as CountOfWorkItems)

Work items can also be counted by using the following:

    /WorkItems?$apply=aggregate(WorkItemId with countdistinct as CountOfWorkItems)


**Return a count of area paths**

    /Areas?$apply=aggregate(AreaId with countdistinct as CountOfAreas)

**Return the sum of all remaining work**

    /WorkItems?$apply=aggregate(RemainingWork with sum as SumOfRemainingWork)

**Return the last work item ID**

    /WorkItems?$apply=aggregate(WorkItemId with max as MaxWorkItemId)

##Group results

Aggregation extensions also support a ```groupby``` clause which is identical to the SQL group by clause. You can use this clause to quickly break down numbers
in more detail.  

For example, the following gives you the count of work items:

    /WorkItems?$apply=aggregate($count as Count)

Add the ```groupby``` clause to return a count of work items by type:

    /WorkItems?$apply=groupby((WorkItemType), aggregate($count as Count))

This returns a result similar to the following:

```JSON
    {
      "@odata.context":"https://{account}.analytics.visualstudio.com/_odata/v1.0/$metadata#WorkItems(WorkItemType,Count)","value":[
	    {
          "@odata.id":null,"WorkItemType":"Bug","Count":3
        },
        {
          "@odata.id":null,"WorkItemType":"Product Backlog Item","Count":13
        }
      ]
    }
```

You can also group by multiple properties as in the following:

    /WorkItems?$apply=groupby((WorkItemType, State), aggregate($count as Count))

This returns a result similar to the following:

```JSON
    {
      "@odata.context": "https://{account}.analytics.visualstudio.com/_odata/v1.0/$metadata#WorkItems(WorkItemType,State,Count)",
      "value": [
        {
          "@odata.id": null,
          "State": "Active",
          "WorkItemType": "Bug",
          "Count": 2
        },
		{
          "@odata.id": null,
          "State": "Committed",
          "WorkItemType": "Bug",
          "Count": 1
        },
        {
          "@odata.id": null,
          "State": "Active",
          "WorkItemType": "Product Backlog Item",
          "Count": 5
        },
		{
          "@odata.id": null,
          "State": "Committed",
          "WorkItemType": "Product Backlog Item",
          "Count": 8
        }
      ]
    }
```

You can also group across entities, however OData grouping differs from how you might normally think about it. 

For example, suppose you wanted to know how many areas are in each project. In OData, "count all areas and group them by project" is equivalent to "give me all projects and a count of areas for each project". This results in a query similar to:

    /Areas?$apply=groupby((Project/ProjectName), aggregate(AreaId with countdistinct as CountOfAreas))

## Filter aggregated results

You can also filter aggregated results, however they are applied slightly differently than when you are not using aggregation. The analytics service evaluates filters along a pipe so it's always best to do the most discrete filtering first. 

Filters look like the following:

    /WorkItems?$apply=filter(Iteration/IterationName eq 'Sprint 89')/filter(WorkItemType eq 'User Story')/groupby((State), aggregate($count as Count))


>[!NOTE]  
>You don't have to provide the ```groupby``` clause. You can simply use the ```aggregate``` clause to return a single value.  


##Multiple aggregations in a single call

When you want to provide multiple pieces of information, such as the sum of completed work and separately the sum of remaining work, you can accomplish this with separate calls or with a single call as follows:  

    /WorkItems?$apply=aggregate(CompletedWork with sum as SumOfCompletedWork, RemainingWork with sum as SumOfRemainingWork)

This will return a result that looks like the following:

```JSON
{
  "@odata.context":"https://{account}.analytics.visualstudio.com/_odata/v1.0/$metadata#WorkItems(SumOfCompletedWork,SumOfRemainingWork)","value":[
    {
      "@odata.id":null,"SumOfCompletedWork":1525841.2900000005,"SumOfRemainingWork":73842.39
    }
  ]
}

```

##Aggregating work items to generate a Cumulative Flow Diagram

Let's say you want to create a [cumulative flow diagram](../guidance/cumulative-flow-cycle-lead-time-guidance.md) in Power BI. You can use a query similar to the one below:

```
https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/WorkItemBoardSnapshot?$apply=filter(DateValue gt 2015-07-16Z and DateValue le 2015-08-16Z)/filter(BoardLocation/BoardName eq 'Stories' and BoardLocation/Team/TeamName eq '{teamName}')/groupby((DateValue, BoardLocation/ColumnName), aggregate(Count with sum as Count))&$orderby=DateValue
```
This returns a result similar to the following:

```JSON
{
  "@odata.context": "https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/$metadata#WorkItemBoardSnapshot(DateValue,BoardLocation(ColumnName),Count)",
  "value": [
    {
      "@odata.id": null,
      "DateValue": "2015-07-16T00:00:00-07:00",
      "Count": 324,
      "BoardLocation": {
        "@odata.id": null,
        "ColumnName": "Completed"
      }
    },
    {
      "@odata.id": null,
      "DateValue": "2015-07-16T00:00:00-07:00",
      "Count": 5,
      "BoardLocation": {
        "@odata.id": null,
        "ColumnName": "In Progress"
      }
    }
  ]
}
```

This result can be directly used by your data visualization of choice.

 Let's take a look at what this query actually does:

* Filters the data to a specific team
* Filters the data to a specific backlog
* Groups the result by Date (in the related Date entity) 
* Groups the result by the ColumnName (in the related BoardLocation entity) 
* Groups the result by the ColumnOrder (in the related BoardLocation entity) 
* Returns a count of work items.

When refreshing Power BI or Excel, the fewer rows required, the faster the refresh occurs.


##Related notes 

- [WIT analytics](wit-analytics.md)  
- [OData Extension for Data Aggregation Version 4.0](http://docs.oasis-open.org/odata/odata-data-aggregation-ext/v4.0/cs01/odata-data-aggregation-ext-v4.0-cs01.html)
