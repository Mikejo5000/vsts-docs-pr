---
title: OData Query Guidelines | VSTS
description: Guidelines for extension developers who want to learn how to write good OData queries.
ms.prod: vs-devops-alm
ms.technology: vs-devops-reporting
ms.assetid: 73E9A63D-B84A-4EA0-9B90-B9BD8BF9646D
ms.manager: trevorc
ms.author: stansw
ms.date: 10/20/2017
---

# OData Query Guidelines

[!INCLUDE [temp](../_shared/analytics-preview.md)]

This section provides guidelines for designing efficient OData queries against Analytics Service. The goal is to help extension developers ensure that the queries have good performance in terms of the execution time and the resource consumption. Queries that do not adhere to these guidelines might provide bad experience when users have to wait long for the reports to be generated or exceed allowed resource consumption and the user get temporarily blocked from the service.

The guidelines are organized as simple recommendations prefixed with the terms **DO**, **CONSIDER**, **AVOID** and **DO NOT**. In certain cases these recommendations were rules enforced in the service and it is reflected by **[BLOCKED]** prefix. These guidelines are intended to help extension developers understand the trade-offs between different solutions. There might be situations where data requirements force you to violate these guidelines. Such cases should be rare, and it is important that you have a clear and compelling reason for your decision.

## Errors and warnings guidelines

### **✔️ DO** review warnings in the OData response.
Every time you execute a query it gets checked against a set of predefined rules. Violations are returned back in the OData response in the `@vsts.warnings`. You should always review these warnings as they provide current and context-sensitive information on how to improve your query.

```json
{
  "@odata.context": "https://{account}.tfsallin.net/_odata/v1.0/$metadata#WorkItems",
  "@vsts.warnings": [
    "The specified query does not include a $select or $apply clause which is recommended for all queries. Details on recommended query patterns are available here: <fwdlink>"
  ],
  ...
}
```

### **✔️ DO** review OData error messages.
Some rules for OData queries were promoted from warning to error level. Instead of being surfaced in the `@vsts.warnings` property they will result in a failed resopnse with 400 (Bad Request) status code. The rule itself will be explained in the `message` property in the Json response. 

```json
{
  "error": {
  "code": "0",
  "message": "The query specified in the URI is not valid. The Snapshot tables in Analytics are intended to be used only in an aggregation. Details on recommended query patterns are available here: <fwdlink>"
  }
}
```

## Restrictions

### **️️✔️ DO** limit the query to the project(s) you have access to.
One of the core principles of Analytics Service is that one query returns the same result for all users of fails in a user does not have permissions to the data. There are no implicit filters added based on who runs the query. One consequence is that you, the query author, have to pay attention to project filters to make sure that the target audince will be able to execute them. If a query tries to access the data in a project for which you do not have access, you will get the following error message.

> *"The query results include data in one or more projects for which you do not have access. Add one or more projects filters to specify the project(s) you have access to in 'WorkItems' entity. If you are using $expand or navigation properties, project filter is required for those entities.*

In order to solve this problem you can either explicitly add a project filter or use the project-scoped endpoint, as explained two sections below.

For example, this query fetches work items that belong to projects identified with either `{projectSK1}` or `{projectSK2}`.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=ProjectSK eq {projectSK1} or ProjectSK eq {projectSK2}
  &$select=WorkItemId, Title
```

### **✔️ DO** specify project filter inside the `$expand` clause if your your expansion could include in data in other, potentially inaccessible projects.
When you expand navigation properties, there is a chance that you will end up referencing data from other, inaccessible projects. Should this happen you will receive the same "*"The query results include data in one or more projects...*" error as in the previous section. Similarly, this problem can be solved by adding explicit project filter to control the expanded data.

This can be done in the regular `$filter` clause for simple navigation properties. For example, the query below explicitly asks for `WorkItemLinks` where both the link and its target exist in the same project.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItemLinks?
  $filter=ProjectSK eq {projectSK} and TargetWorkItem/ProjectSK eq {projectSK}
  &$select=LinkTypeReferenceName, SourceWorkItemId, TargetWorkItemId
  &$expand=TargetWorkItem($select=WorkItemId, Title)
```

Alternatively, you could move the filter to `$filter` expand option in the `$expand` clause. However, it changes the semantic of the query. For example, the query below gets all the links from a given project and conditionally expands target only if it exists in the same project. Although valid, this approach might lead to some confusion as it might be hard to tell wether a property is not expanded because it is `null` or because it was filtered out. Please use this solution only if you really need this particular behavior.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItemLinks?
  $filter=ProjectSK eq {projectSK}
  &$select=LinkTypeReferenceName, SourceWorkItemId, TargetWorkItemId
  &$expand=TargetWorkItem($filter=ProjectSK eq {projectSK}; $select=WorkItemId, Title)
```

Filtering with `$filter` expand option is very useful when you expand collection property such as `Children` in `WorkItems` entity set. For example, the query below gets all work items from a given project together with all their children which belong in the same project.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=ProjectSK eq {projectSK}
  &$select=WorkItemId, Title
  &$expand=Children($filter=ProjectSK eq {projectSK}; $select=WorkItemId, Title)
```

You do need to specify the filter if you expand one of the following properties:
* `WorkItems` entity set: `Parent`, `Children`.
* `WorkItemLinks` entity set: `TargetWorkItem`.

### **️️✔️ CONSIDER** accessing project-scoped endpoint.
Previous two sections explained how to explicitly define filters to restrict the data to selected projects. If you are interested in the data from a only one project there is an easier solution. If you use the project-scoped OData endpoint (`/{project}/_odata/v1.0`), then the project filter will be implicitly applied to referenced entity set as well as all the expanded navigation properties.

With this simplification the queries from the previous section could be rewritten to the following form. Please notice that not only did the filter in expand clause dissapear, but also the filter on the main entity set is no longer needed.
```odata
https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/WorkItemLinks?
  &$select=LinkTypeReferenceName, SourceWorkItemId, TargetWorkItemId
  &$expand=TargetWorkItem($select=WorkItemId, Title)
```

Query for work item children is also much shorter and simpler.
```odata
https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/WorkItems?
  &$select=WorkItemId, Title
  &$expand=Children($select=WorkItemId, Title)
```

This solution can only be applied if you are interested in the data from a single project. For cross-project reporting you have to use filtering strategies described in the previous sections.

### **️️✔️ DO** wait or stop the operation if your query exeeded usage limits.
If you execute a lot of queries or the queries require a lot of resources to run you might exceed the limits and get temporarily blocked. Should this happen, please stop the operation as chances are that the next query you send will fail with the same error message.

> *Request was blocked due to exceeding usage of resource '{resource}' 
in namespace '{namespace}'.*

For more information on rate limiting, see "Rate limits" topic. 
To learn more about how to design efficient OData queries please refer to [Performance Guidelines](#performance-guidelines) section.


### **❌ [BLOCKED] DO NOT** use snapshot entities for anything other than aggregations.
<a name="odata_snapshot_without_aggregation"></a>
Snapshot entity sets with `Snapshot` suffix are special because they are modelled as *daily snapshots*. This means they can be used to get a state of entities as they were at the end of each day in the past. For example if you queried `WorkItemSnapshot` and filter to a single `WorkItemId` you would get one record for each day since the work item was created. Of course loading directly all of this data would be very expensive and most likely would exceed usage limits, thus, it is blocked. Aggregations on these entities, on the other hand, are both allowed and recommended. In fact, these tables were designed with aggregation scenarios in mind.

For example, the query below gets the number of work items as by date to observe how it grew in January 2017.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItemSnapshot?
  $apply=
    filter(DateSK ge 20170101 and DateSK le 20170131)/
    groupby((DateSK), aggregate($count as Count))
```


### **✔️ DO** include `DateSK` or `DateValue` column in `groupby` clause when you aggregate over snapshot tables.
Since all snapshot entities are modelled as ***daily snapshot tables*** you should always include one of the day properties (`DateSK` or `DateValue`) in the groupping clause. Otherwise result may seem incorrectly inflated. For example if you groupped `WorkItemSnaphost` only by `AssignedTo` property and aggregate it with count, all the numbers of work items assigned to people would be multiplied by the number of days when such assignment was active. There might be some situations where this is a desired outcome, but such cases are very rare.


### **❌ [BLOCKED] DO NOT** use entity keys in resouce paths for entity addressing.
OData syntax provides a way to access a particular entity by to including its keys directly in the URL sements as described in the specification - [OData Version 4.0. Part 2: URL Conventions - 4.3 Addressing Entities](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part2-url-conventions/odata-v4.0-errata03-os-part2-url-conventions-complete.html#_Toc453752340). Although allowed in OData, such addressing has been completely blocked in Analytics Service. If you try to use it, you will get the following error.

> *The query specified in the URI is not valid. The Analytics Service doesn't support key or property navigation like WorkItems(Id) or WorkItem(Id)/AssignedTo. If you getting that error in PowerBI, please, rewrite your query to avoid incorrect folding that causes N+1 problem.*

As the error messages hints, direct entity addressing can be abused by certain client tools. Instead of loading all the data in a single request such clients might choose to query for each entity independently. This might result in very high number of requests and is strongly discouraged. A much better approach is using explicit entity addressing as explained in the following section.


### **✔️ DO** explicitly address entities with filter clauses.
If you want to fetch data for a single entity you should use the same approach as for a collection of entities and explicitly define filters in the `$filter` clause.

For example, the query below gets a single work item by its identifier.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=WorkItemId eq {id}
  &$select=WorkItemId, Title
```

If you are not sure which properties should be included in such filter, you can look it up in the metadata. They will be listed in the `Key` element of the `EntityType`. For example `WorkItemId` and `Revision` are key columns for the `WorkItemRevision` entity.
```xml
<EntityType Name="WorkItemRevision">
  <Key>
    <PropertyRef Name="WorkItemId"/>
    <PropertyRef Name="Revision"/>
  </Key>
  [...]
</EntityType>
```


### **❌ [BLOCKED] DO NOT** expand `Revisions` on `WorkItem` entity.
Data model does disallow certain types of expansions. One of them, which might be surprising to some, is the `Revisions` collection property on the `WorkItem` entity. If you try expand this property you will receive the following error message.

> *The query specified in the URI is not valid. The property 'Revisions' cannot be used in the $expand query option.*

This restriction was put in place to encourage everyone to the recommended solution, which is fetching revisions from `WorkItemRevisions` as it is explained in the following section.


### **✔️ DO** use `WorkItemRevisions` entity set to load all the revisions for a given work item.
You should use `WorkItemRevisions` each time you want to fetch full history for a work item or a collection of work items. 

For example, the query below gets all the revisions of a work item with `{id}` identifier.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItemRevisions?
  $filter=WorkItemId eq {id}
  &$select=WorkItemId, Title
```

If you care about full history for all the work items that match certain criteria, you can express it using a filter on `WorkItem` navigation property. For example, the query below gets all the revisions of all the work items which are currently active.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItemRevisions?
  $filter=WorkItem/State eq 'Active'
  &$select=WorkItemId, Title
```

### **❌ [BLOCKED] DO NOT** group on distinct columns.
<a name="odata_query_distinct_columns_in_last_groupby"></a>
Groupping operation is intended to reduce the number of records. Using distinct columns in the `groupby` clause is a clear indication of a problem in a query and it will fail immediately. Should you accidentially run into that situation you will receive the following error message. In order to resolve this problem you should remove the distinct column from the groupig clause.

>*One or more of the columns specified in the groupby clause of this query are not recommended.*


### **✔️ DO** use batch endpoint for long queries.
Sometimes you may run into problems with very long queries. This can happen when you work with project with a lot of custom fields or your query gets constructed programatically. The current limit for OData queries sent with `HTTP GET` is 3000 characters. If you you exeed it, you will get "*404 Not Found*" response back.

```http
HTTP/1.1 404 Not Found
Content-Length: 0
```

You can solve this problem by using the OData batch endpoint as explained in the specification - [OData Version 4.0. Part 1: Protocol - 11.7 Batch Requests](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part1-protocol/odata-v4.0-errata03-os-part1-protocol-complete.html#_Toc453752313). Batch capability was primary designed to group multiple operations into a single `HTTP` request payload, but it can also be used as a workaround for the query length limitation. By sending a `HTTP POST` request you can pass a query of an arbitrary lenght and it will be correctly interpreted by se service. 


### **❌ [BLOCKED] DO NOT** use batch endpoint for sending multiple queries.
>[!IMPORTANT] Not ready for review.

Yes, batch endpoint is not for batching multiple requests. The only reason why it was exposed was to support very long queries. As of right now it requires the response to contain exactly one query.

### **❌ AVOID** creating very long queries.
>[!IMPORTANT] Not ready for review.

Just because you can, it does not mean you should.
https://stackoverflow.microsoft.com/questions/41401/suggestion-for-massive-filter-on-bugs

### **✔️ DO** specify time zone when filtering on date columns.
>[!IMPORTANT] Not ready for review.

https://stackoverflow.microsoft.com/questions/21550/date-filters-using-the-analytics-service-return-a-no-coercion-operator-is-defin

## Performance guidelines

### **✔️ DO** specify columns in `$select` clause
You should speciy the columns you care about in the `$select` clause. This decreases the number of columns that have to be scanned and reduces the size of the response payload.

For example, the query below specifies the columns for work items.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $select=WorkItemId, Title, State
```

> [!NOTE]
> Visual Studio Team Services supports process customization. Some account administrators use this feature and create hundreds of custom fields. If you omit the `$select` clause, all of these fields will be returned.


### **✔️ DO** specify columns in `$select` expand option inside the `$expand` clause.
Similarly to `$select` clause guidelines, you should also specify the columns in `$select` expand option in the `$expand` clause. It is easy to forget, but if you omit it, response will contain all the columns from the expanded object.

For example, the query below specifies the columns for both the work item and its parent.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $select=WorkItemId, Title, State
  &$expand=Parent($select=WorkItemId, Title, State)
```


### **✔️ DO** define a filter on `RevisedDateSK` when you write historical queries agains work items entity sets.
When you query for historical data, the chances are that you are interested in the most recent period (e.g. 30 days, 90 days). Due to how work items entities were implemented there is a convenient way you can write such queries to get great performance. Each time you update a work item it creates a new revision and records this action in `System.RevisedDate` colum. This makes it perfect for history filters.

In Analytics Servcie revised date is represented by `RevisedDate` (`Edm.DateTimeOffset`) and `RevisedDateSK` (`Edm.Int32`). For best performance you should use the latter. This is date *surrogate key* and it represents the date when revision was create or it might have null for active revisions. If you know that you are interested in all the dates since `{startDate}` inclusive, you should add the following filter to your query.

```
RevisedDateSK eq null or RevisedDateSK gt {startDateSK}
```

For example, the query below returns the number of work items for each day since the beginning of 2017. Please notice that apart from the obvious filter on `DateSK` column there is second filter on `RevisedDateSK`. Although it may seem redundant, it helps query engine filter out revisions taht are not in scope and sigificantly improves performance of the query.
```odata
https://tseadm.analytics.visualstudio.com/_odata/v1.0/WorkItemSnapshot?
  $apply=
    filter(DateSK gt 20170101)/
    filter(RevisedDateSK eq null or RevisedDateSK gt 20170101)/
    groupby(
      (DateValue), 
      aggregate($count as Count)
    )
```

> [!NOTE]
> We came up with this recommendation when were working on Burndown widgets. Initially we defined filters only for `DateSK` but we could not get this query to scale well to very large accounts. During query profiling we noticed that `DateSK` does not filter revisions well. Only after we did add a filter on `RevisedDateSK` we were able to get great performance at scle.
> <br>~ *Product Team*

### **✔️ DO** use weekly or monthly snapshots when your historical query spans long time range.
By default all the snapshot tables are modelled as *daily snapshot fact* tables. Consequently, if you query for a time range will get a value for each day. For long time ranges this result in a very large number of records. If you do not need such high precision you can use weekly or even monthly snapshots. This can be achieved by adding additional filter expression to remove days which do not finish a given week or monnth. In Analytics Service there is `IsLastDayOfPeriod` property, which was added with this sceario in mind. This property is of type `Microsoft.VisualStudio.Services.Analytics.Model.Period` and can tell if day finishes different periods (e.g. weeks, months, etc).

```xml
<EnumType Name="Period" IsFlags="true">
  <Member Name="None" Value="0"/>
  <Member Name="Day" Value="1"/>
  <Member Name="WeekEndingOnSunday" Value="2"/>
  <Member Name="WeekEndingOnMonday" Value="4"/>
  <Member Name="WeekEndingOnTuesday" Value="8"/>
  <Member Name="WeekEndingOnWednesday" Value="16"/>
  <Member Name="WeekEndingOnThursday" Value="32"/>
  <Member Name="WeekEndingOnFriday" Value="64"/>
  <Member Name="WeekEndingOnSaturday" Value="128"/>
  <Member Name="Month" Value="256"/>
  <Member Name="Quarter" Value="512"/>
  <Member Name="Year" Value="1024"/>
  <Member Name="All" Value="2047"/>
</EnumType>
```

Since `Microsoft.VisualStudio.Services.Analytics.Model.Period` is defined as and enum with flags, you should use [`has`](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part2-url-conventions/odata-v4.0-errata03-os-part2-url-conventions-complete.html#_Toc444868681) operator and specify full type for the period literals.
```odata
IsLastDayOfPeriod has Microsoft.VisualStudio.Services.Analytics.Model.Period'Month'
```

For example, the query below returns the number of work items as it was on the last day of each month.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItemSnapshot?
  $apply=
    filter(IsLastDayOfPeriod has Microsoft.VisualStudio.Services.Analytics.Model.Period'Month')/
    groupby(
      (DateValue), 
      aggregate($count as Count)
    )
```

### **✔️ DO** use `Tags` collection property on work items when filtering by tags.
>[!IMPORTANT] Not ready for review.

There is property `TagNames` which one could use with `contains` function to find the right work items, but for better performance and accurate results you should use `Tags` navigation property.

```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=Tags/any(t:t/TagName eq '{tag}')
```
https://stackoverflow.microsoft.com/questions/18172/how-to-query-work-items-for-multiple-tags

### **✔️ CONSIDER** using `TagNames` property on work items in `$select` clauses.
>[!IMPORTANT] Not ready for review.

Property `TagNames` is very useful in `$select` clauses.


### **❌ DO NOT** use unbounded expansion (`$levels=max`)
>[!IMPORTANT] Not ready for review.

### **✔️ CONSIDER** writting query to return small number of records.
>[!IMPORTANT] Not ready for review.

### **✔️ CONSIDER** limiting the number of selected columns to minimum.
<a name="ODATA_QUERY_TOO_WIDE"></a>
>[!IMPORTANT] Not ready for review.

### **✔️ CONSIDER** filterig on date surrogate key columns with DateSK suffix.
>[!IMPORTANT] Not ready for review.

```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=CreatedDateSK eq {createdDateSK}
```

### **✔️ CONSIDER** filterig on surrogate key columns.
If you want to filter the data on the value of related object (e.g. filtering work item on project name) you always have two choices. You can either use the navigation property (e.g. `Project/ProjectName`) or capture the *surrogate key* up-front and use it directly in the query (e.g. `ProjectSK`). If you are building a widget you should always prefer the latter option. When the key is passed as part of the query the number of entity sets that have to be touched goes down and the performance improves.

For example, the query below filters `WorkItems` using `ProjectSK` property rather than `Project/ProjectName` navigation property.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=ProjectSK eq {projectSK}
```

### **❌ AVOID** using Parent, Child or Revision properties in a `$filter` or `$expand` clauses
<a name="ODATA_QUERY_PARENT_CHILD_RELATIONS"></a>
>[!IMPORTANT] Not ready for review.

### **✔️ CONSIDER** passing `VSTS.Analytics.MaxSize` preference in the header.
When you execute a query you don't know how many records there are to retrieve. You have to either send anotehr query with aggregations or follow all the next links and fetch the entire dataset. Analytics Service respects `VSTS.Analytics.MaxSize` preference, which lets you fail fast should the dataset be bigger than what your client can accept. This option is particularly helpful in the data export scenarios. In order to use it you have to add `Prefer` header to your HTTP request and set `VSTS.Analytics.MaxSize` to a non-negative value which represents the max number of records you can accept. If you set it to zero, then a default value of 200k will be used.

For example, the query below returns work items provided that the dataset is smller or equal to 1000 records.
```http
GET https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems HTTP/1.1
User-Agent: Microsoft.Data.Mashup
Prefer: VSTS.Analytics.MaxSize=1000
OData-MaxVersion: 4.0
Accept: application/json;odata.metadata=minimal
Host: {account}.analytics.visualstudio.com
```

### **❌ AVOID** sending more requests after you received a timeout error.
>[!IMPORTANT] Not ready for review.

https://stackoverflow.microsoft.com/questions/41065/how-do-i-resolve-error-the-request-has-exceeded-request-timeout-please-try-aga
```
message: "TF400733: The request has been canceled: The request has exceeded request timeout, please try again.",
```       


## Query style guidelines

### **✔️ DO** use `$count` virtual property in the aggregation methods.
Some entities expose `Count` property. They make some reporting scenarios easier when the data gets exported to a different storage. However, you should not use these columns in aggregations in OData queries. Please use `$count` virtual property instead.

For example, the query below returns the total number of work items.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $apply=aggregate($count as Count)
```


### **❌ AVOID** using `$count` virtual property in the URL segment.
Although OData standard allows you to use `$count` virtual property for entity sets (e.g. `_odata/v1.0/WorkItems/$count`), not all clients can interpret the response correctly. Therefore, it is recommended to use aggregations instead.

For example, the query below returns the total number of work items.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $apply=aggregate($count as Count)
```


### **❌ AVOID** mixing `$apply` and `$filter` clauses in the same query.
`$apply` has precendence over `$filter`, thus, mixing them, might lead to unexpected results.

```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $apply=
  filter(StoryPoints gt 2)
  /groupby(
    (Area/AreaPath),
    aggregate(StoryPoints with sum as StoryPoints)
  )
  &$filter=StoryPoints gt 5
```



### **✔️ CONSIDER** using parameter aliases to separate volatile parts of the query.
>[!IMPORTANT] Not ready for review.

[OData Version 4.0. Part 2: URL Conventions - 5.1.1.13 Parameter Aliases](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part2-url-conventions/odata-v4.0-errata03-os-part2-url-conventions-complete.html#_Toc444868740)


### **✔️ CONSIDER** structuring your query to match the OData evaluation order.
>[!IMPORTANT] Not ready for review.

In summary, start with $appply and.


### **✔️ CONSIDER** reviewing OData capabilities described in the metadata annotations.
When you are not sure about which OData capabilities are available in Analytics Service you should look up annotations in the metadata.
The list of available annotation is maintained by the [OASIS Open Data Protocol (OData) Technical Committee](https://www.oasis-open.org/committees/odata/) in a [TC GitHub repository](https://github.com/oasis-tcs/odata-vocabularies/blob/master/vocabularies/Org.OData.Capabilities.V1.md).

For example, the list of supported filter functions is available in `Org.OData.Capabilities.V1.FilterFunctions` annotation on the entity container.

```xml
<Annotation Term="Org.OData.Capabilities.V1.FilterFunctions">
  <Collection>
  <String>contains</String>
  <String>endswith</String>
  [...]
  </Collection>
</Annotation>
```

Another useful annotation is `Org.OData.Capabilities.V1.ExpandRestrictions`, which explains which navigation properties cannot be used in the `$expand` clause. For example, the following annotation expalins that `Revisions` in `WorkItems` entity set cannot be expanded.

```xml
<EntitySet Name="WorkItems" EntityType="Microsoft.VisualStudio.Services.Analytics.Model.WorkItem">
  [...]
  <Annotation Term="Org.OData.Capabilities.V1.ExpandRestrictions">
    <Record>
      <PropertyValue Property="Expandable" Bool="true"/>
      <PropertyValue Property="NonExpandableProperties">
        <Collection>
          <NavigationPropertyPath>Revisions</NavigationPropertyPath>
        </Collection>
      </PropertyValue>
    </Record>
  </Annotation>
</EntitySet>
```
