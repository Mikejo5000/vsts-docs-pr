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

**VSTS**  
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
    "The specified query does not include a $select or $apply clause which is recommended for all queries."
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
  "message": "The query specified in the URI is not valid. The Snapshot tables in Analytics are intended to be used only in an aggregation."
  }
}
```

## Restrictions guidelines

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

> *Request was blocked due to exceeding usage of resource '{resource}' in namespace '{namespace}'.*

For more information on rate limiting, see "Rate limits" topic. 
To learn how to design efficient OData queries please refer to [Performance Guidelines](#performance-guidelines) section.


### **️️✔️ DO** wait or stop the operation if your query fails with a timeout.
<a name="question-41065"></a>
Similarly to esceeding usage limits, you should wait or stop the operation if your query hits timeout. There is a chance that this is transient problem and it makes sense to retry once, but if the timeouts are persisting the query is probably too expensive to run and retrying will only result in exceeding usage limits and you will get blocked.

> *TF400733: The request has been canceled: The request has exceeded request timeout, please try again.*

Timeout is a good indication that the query is expensive and should be optimized. To learn how to design efficient OData queries please refer to [Performance Guidelines](#performance-guidelines) section.


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


### **❌ AVOID** aggregations that can result in arithmetic overflow.
In rare cases you may run into problems with arithmetic overflow in the aggregation queries. For example, this can happen when you sum some numeric properties which are not intended for summarization such as `StackRank` in the work item entities. Since [OData Extension for Data Aggregation](http://docs.oasis-open.org/odata/odata-data-aggregation-ext/v4.0/cs01/odata-data-aggregation-ext-v4.0-cs01.html) standard does not provide a way to cast a property to a different type, the only way to solve this problem is to remove the problematic property from the aggregation.


### **✔️ DO** use batch endpoint for long queries.
Sometimes you may run into problems with very long queries. This can happen when you work with project with a lot of custom fields or your query gets constructed programatically. The current limit for OData queries sent with `HTTP GET` is 3,000 characters. If you you exeed it, you will get "*404 Not Found*" response back.

```http
HTTP/1.1 404 Not Found
Content-Length: 0
```

You can solve this problem by using the OData batch endpoint as explained in the specification - [OData Version 4.0. Part 1: Protocol - 11.7 Batch Requests](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part1-protocol/odata-v4.0-errata03-os-part1-protocol-complete.html#_Toc453752313). Batch capability was primary designed to group multiple operations into a single `HTTP` request payload, but it can also be used as a workaround for the query length limitation. By sending a `HTTP POST` request you can pass a query of an arbitrary lenght and it will be correctly interpreted by se service. 


### **❌ [BLOCKED] DO NOT** use batch endpoint for sending multiple queries.
<a name="odata_batch_query_size_invalid"></a>
The batch endpoint was exposed primary to make it possible to send long queries. Its capabilities for handling a batch of multiple requests are restricted. Single request can still have only one query. If you try to send a batch of several queries the operation will fail with the following error message. The only solution is to split queries into multiple requests.

> *The Analytics Service doesn’t support processing of multiple operations which the current batch message contains. The Analytics Service uses OData batch in order to support POST requests, but requires you limit the operation to a single request.*

### **❌ AVOID** creating very long queries.
<a name="question-41401"></a>
Whenever you create a very long query you should question whether it is really necessary. There are many scenarios where long query is absolutely necessary (e.g. very complex filters or long list of properties), but typically they are an early indicator of a suboptimal design. That is why when you notice it, you shoud stop and reevaluate your approach.

If the length is driven by the fact that you are including a lot of entity keys in the query (e.g. `WorkItemId eq {id 1} or WorkItemId eq {id 2} or ...`), then you can probably rewrite it. Instead of passing the identifiers try to define some other criteria that will select the same set of entities. Sometimes it might be necessary to modify your process (e.g. add a new field or tag), but it is typically worth it. Using more abstract filters the query will be easier to maintain and has potential to reach better performance.

Another scenario that can lead you to a long query is including a lot of individual dates (e.g. `DateSK eq {dateSK 1} or DateSK eq {dateSK 2} or ...`). Similarly to the previous case, the chances are that there is some other pattern that can be used to create more abstract filter. For example, The query below gets all the work items which were created on Monday.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=CreatedOn/DayOfWeek eq 2
  &$select=WorkItemId, Title, State
```

### **✔️ DO** specify time zone when filtering on date columns.
All the date and time information is exposed with a time zone (`Edm.DateTimeOffset`) and an offset that matches account time zone settings. This is great as the data is precise and simple to interpret at the same time. Another consequence, which might be not so obvious, is that all the filters have to pass the time zone information as well. If you skip it, you will get the following error message.

> *The query specified in the URI is not valid. No datetime offset was specified.  Please use either of these formats YYYY-MM-ddZ to specify everything since midnight or yyyy-MM-ddThh:mm-hh:mm (ISO 8601 standard representation of dates and times) to specify the offset.*

The error message explains it well. The only thing you need to do solve this problem is adding the time zone information. For example, assuming that the account is configured to display data in "*(UTC-08:00) Pacific Time (US & Canada)*" time zone, the following query gets all the work items created since the beginning of 2017.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=CreatedDate ge 2017-01-01T00:00:00-08:00
  &$select=WorkItemId, Title, State
```

The same solution works for time zones with positive offsets, however, plus character (`+`)  has a special meaning in the URI and it has to be handled accordingly. If you specify `2017-01-01T00:00:00+08:00` (with a `+` character) as your starting point you will get the following error.

> *The query specified in the URI is not valid. Syntax error at position 31 in 'CreatedDate ge 2017-01-01T0000 08:00'.*

To solve it you need to replace `+` character with its encoded version - `%2B`. For example, assuming that the account is configured to display data in "*(UTC+08:00) Beijing, Chongqing, Hong Kong, Urumqi*" time zone, the following query gets all the work items created since the beginning of 2017.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=CreatedDate ge 2017-01-01T00:00:00%2B08:00
  &$select=WorkItemId, Title, State
```

Alternative approach is to use date surrogate key properties as they do not keep the time zone information. For example, the following query gets all the work items created since the beginning of 2017 regardless the account settings.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=CreatedDateSK ge 20170101
  &$select=WorkItemId, Title, State
```


## Performance guidelines

### **✔️ DO** measure the impact of implementing a performance guideline.
As with any performance recommendations you should not blindly implement them. Instead, always capture the baseline and **measure** the impact of changes you make. All of the guidelines were created based on the interactions with clients of Analytis Service who had very specifc requirements and challenges. These recommendations were consider general and potentially useful for anyone who designs similar queries. However, in rare cases, following the guidelines could have none or even negative effect on the performance. You do need to measure the difference to notice it. Should this happen please provide a feedback in the [Developer Community](https://developercommunity.visualstudio.com/spaces/21/index.html) portal.

There are many options to measure the performance. The simplest one is running two versions of the same query directly in the browser and observing time taken in the developer tools. For example, you can use [Network panel](https://docs.microsoft.com/en-us/microsoft-edge/f12-devtools-guide/network#network-request-list) in [Microsoft Edge F12 Developer Tools](https://docs.microsoft.com/en-us/microsoft-edge/f12-devtools-guide)). Another option is to capture this information using [Fiddler Web Debugger Tool](https://msdn.microsoft.com/en-us/library/windows/desktop/ff966510(v=vs.85).aspx). Regardless the solution you should run both queries multiple times (e.g. 30 runs each) to have a sufficiently large sample to reason about performance characteristics. Please notice that Analytics Service follows multi-tenant architecture, thus, duration of your queries might be impacted by the other operations happening at the same time. 


### **✔️ DO** use aggregation extensions.
By far the best thing you can do to improve performance of your queries is to use aggregation extension - [OData Extension for Data Aggregation](http://docs.oasis-open.org/odata/odata-data-aggregation-ext/v4.0/cs01/odata-data-aggregation-ext-v4.0-cs01.html). This allows you to ask the service to summarize data server-side and return response which is much smaller than what you would need to fetch if you wanted to apply the same function client-side. Finally, Analytics Service is optimized for this type of queries, so please make use of it.


### **✔️ DO** specify columns in `$select` clause.
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


### **✔️ DO** define a filter on `RevisedDateSK` when you query for historical work items data (`WorkItemRevisions` or `WorkItemSnapshot` entity sets).
When you query for historical data, the chances are that you are interested in the most recent period (e.g. 30 days, 90 days). Due to how work items entities are implemented there is a convenient way for you to write such queries to get great performance. Each time you update a work item it creates a new revision and records this action in `System.RevisedDate` field, which makes it perfect for history filters.

In Analytics Servcie, the revised date is represented by `RevisedDate` (`Edm.DateTimeOffset`) and `RevisedDateSK` (`Edm.Int32`) properties. For best performance you should use the latter. This is date *surrogate key* and it represents the date when revision was create or it has `null` for active, uncompleted revisions. If you know that you are interested in all the dates since `{startDate}` inclusive, you should add the following filter to your query.

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
<a name="question-18172"></a>
There is property `TagNames` which one could use with `contains` function to check if a work it was marked with a specific tag. This approach, however, might result in a slow queries especially when checking for multiple tags at the same time. For best performance and accurate results you should use `Tags` navigation property.

For example, the query below gets all the work items which were tagged with a `{tag}`.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=Tags/any(t:t/TagName eq '{tag}')
  &$select=WorkItemId, Title, State
```

This approach also works great when you need to filter on multiple tags. For example, the query below gets all the work items which were tagged with `{tag1}` **or** `{tag2}`

```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=Tags/any(t:t/TagName eq {tag1} or t/TagName eq {tag2})
  &$select=WorkItemId, Title, State
```

You can also combine these filters with an "and" operator. For example, the query below gets all the work items which were tagged with both `{tag1}` **and** `{tag2}`
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=Tags/any(t:t/TagName eq {tag1}) and Tags/any(t:t/TagName eq {tag2})
  &$select=WorkItemId, Title, State
```


### **✔️ DO** use `TagNames` property if you want to display all the tags on a work item as text.
Navigation property `Tags`, described in the previous section, is great for filtering. However, it might be challenging to work with it as the tags are returned in a nested collection. Data model has also `TagNames` primitive property (`Edm.String`), which was added to simplify tags consumption scenarios. It is a single text value which contains a list of all the tags combined with "; " separator. It is perfect when all you care about is displaying tags together. Of course you can combine it with the tags filters described previously.

For example, the query below gets all the work items which were tagged with a `{tag}`. The information it gets is identifer, title, state and a text representation of combined tags.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=Tags/any(t:t/TagName eq '{tag}')
  &$select=WorkItemId, Title, State, TagNames
```

### **❌ DO NOT** use `tolower` and `toupper` functions to perform case-insensitive comparison.
Working with other systems you might expect you need to use `tolower` or `toupper` functions for the case-insensitive comparison. With Analytis Servie all the sting comparison is case-insensitive by default, thus you do not need to apply any functions to explicitly handle it.

For example, the following query gets all the work items tagged with "QUALITY", "quality" or any other case combination of this word.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=Tags/any(t:t/TagName eq 'quality')
  &$select=WorkItemId, Title, State, TagNames
```


### **❌ DO NOT** use unbounded expansion with `$levels=max`
OData has a interesting capability of expanding all the levels of a hierarchical structure. In Analytics Service there exists some entities where such unbounded expansion could be applied. This operation does work only for really small accounts because it does not scale well with the account size. Please do not use it at all if you are working with large accounts or you are developing a widget and you have no control over where it is going to be installed.


### **✔️ DO** use server-driven paging.
If you ask for a set that is too large to be sent in a single response Analytics Service will apply paging. The response will include only a partial set and a link that allows retrieving the next partial set of items. This strategy is described in the OData specifiction - [OData Version 4.0. Part 1: Protocol - Server-Driven Paging](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part1-protocol/odata-v4.0-errata03-os-part1-protocol-complete.html#_Server-Driven_Paging). By letting the service control the paging you get the best performance as the `skiptoken` has been carefully design for each entity to be as efficient as possible.

The link to the next page is included in the `@odata.nextLink` property.
```json
{
  "@odata.context": "https://{account}.analytics.visualstudio.com/_odata/v1.0/$metadata#WorkItems(*)",
  "value": [
    ...
  ],
  "@odata.nextLink":"https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?$skiptoken=12345"}
```


### **❌ DO NOT** use `$top` and `$skip` query options to implement client-driven paging.
Working with other REST API's you might want to implement client-driven paging with `$top` and `$skip` query options. Please do not do it. There are several problems with this approach and performance is one of them. Instead please adopt the server-driven paging strategy explained in the previous section.


### **✔️ CONSIDER** writting query to return small number of records.
This is probably the most intuitive guideline. You should always aim to fetch only the data you really care about. This can be achieved by making most of the powerful filtering capabilities available in OData query language.


### **✔️ CONSIDER** limiting the number of selected properties to minimum.
<a name="odata_query_too_wide"></a>
Some project administrators havily customize their processes by adding custom fields. This can lead to performance issues when fetching all the available columns on very wide entities (e.g. `WorkItems`). Please notice that Analytics Service is built on top of a *Columnstore Index* technology which means that data is both storage and query processing is column-based. Therefore, the more properties are refernced in the query, the more expensive it is going to be. You should always aim to limit the set of properties to what you really care about in your reporting scenario.


### **✔️ CONSIDER** filterig on date surrogate key properties (`DateSK` suffix).
There are many ways you can define a date filter. You can filter on the date property directly (e.g. `CreatedDate`), its navigation counterpart (e.g. `CreatedOnDate`) or its surrogate key representation (e.g. `CreatedDate`). The last option yields the best performance and should always be preffered if the reporting requirements allow for it.

For example, the query below gets all the work items created since the beginning of 2017.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=CreatedDateSK ge 20170101
```


### **✔️ CONSIDER** filterig on surrogate key columns.
If you want to filter the data on the value of related object (e.g. filtering work item on project name) you always have two choices. You can either use the navigation property (e.g. `Project/ProjectName`) or capture the *surrogate key* up-front and use it directly in the query (e.g. `ProjectSK`). If you are building a widget you should always prefer the latter option. When the key is passed as part of the query the number of entity sets that have to be touched goes down and the performance improves.

For example, the query below filters `WorkItems` using `ProjectSK` property rather than `Project/ProjectName` navigation property.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=ProjectSK eq {projectSK}
```


### **❌ AVOID** using `Parent`, `Children` or `Revisions` properties in the `$filter` or `$expand` clauses.
<a name="odata_query_parent_child_relations"></a>
Work items are the most expensive entities in the whole model. They have several navigation properties that can be used to access related work items: `Parent`, `Children`, `Revisions`. Every time you use them in your queries you should expect performance decline. Therefore, you should always question if they are necessary and potentially update your design. For example, instead of expanding `Parent` you can fetch more work items and use `ParentWorkItemId` property to recostruct the full hiearchy client-side. Such optimization has to be done on the case-by-case basis.


### **✔️ CONSIDER** passing `vsts.analytics.maxsize` preference in the header.
When you execute a query you don't know how many records there are to retrieve. You have to either send anotehr query with aggregations or follow all the next links and fetch the entire dataset. Analytics Service respects `vsts.analytics.maxsize` preference, which lets you fail fast should the dataset be bigger than what your client can accept. This option is particularly helpful in the data export scenarios. In order to use it you have to add `Prefer` header to your HTTP request and set `vsts.analytics.maxsize` to a non-negative value which represents the max number of records you can accept. If you set it to zero, then a default value of 200k will be used.

For example, the query below returns work items provided that the dataset is smller or equal to 1000 records.
```http
GET https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems HTTP/1.1
User-Agent: Microsoft.Data.Mashup
Prefer: vsts.analytics.maxsize=1000
OData-MaxVersion: 4.0
Accept: application/json;odata.metadata=minimal
Host: {account}.analytics.visualstudio.com
```


## Query style guidelines

### **✔️ DO** use `$count` virtual property in the aggregation methods.
Some entities expose `Count` property. They make some reporting scenarios easier when the data gets exported to a different storage. However, you should not use these columns in aggregations in OData queries. Please use `$count` virtual property instead.

For example, the query below gets the total number of work items.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $apply=aggregate($count as Count)
```


### **❌ AVOID** using `$count` virtual property in the URL segment.
Although OData standard allows you to use `$count` virtual property for entity sets (e.g. `_odata/v1.0/WorkItems/$count`), not all clients can interpret the response correctly. Therefore, it is recommended to use aggregations instead.

For example, the query below gets the total number of work items.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $apply=aggregate($count as Count)
```


### **✔️ CONSIDER** using parameter aliases to separate volatile parts of the query.
Parameter aliases provide an elegant solution to extract volatile parts such as parameter values from the main query text. They can be used in of expressions that evaluate to a primitive value, a complex value, or a collection of primitive or complex values as explained in the specification - [OData Version 4.0. Part 2: URL Conventions - 5.1.1.13 Parameter Aliases](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part2-url-conventions/odata-v4.0-errata03-os-part2-url-conventions-complete.html#_Toc444868740). Parameters are particularly useful when the query text is used as a template that can be instantiated with user supplied values.

For example, the following query uses `@createdDateSK` parameter to separate the value from the filter expression.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=CreatedDateSK ge @createdDateSK
  &$select=WorkItemId, Title, State
  &@createdDateSK=20170101
```


### **❌ AVOID** mixing `$apply` and `$filter` clauses in a single query.
If you want to add filter to your query you have two options. You can either do it with `$filter` clause or `$apply=filter()` combination. Each one of these options works great on its own, but combining them together might lead to some unexpected results. Despite the expectation one might have, OData clearly defines an order of the evaluation and `$apply` clause has priority over `$filter`. For this reason, you should choose one or another but avoid these two filter option in a single query. This is particularly important if the queries are generated automatically.

For example, the query below first filters work items by `StoryPoint gt 5`, aggregates result by are path and finally filters the result by `StoryPoints gt 2`. Withi this evaluation order the query will always return an empty set.
```odata
https://{account}.analytics.visualstudio.com/_odata/v1.0/WorkItems?
  $filter=StoryPoints gt 2
  $apply=
    filter(StoryPoints gt 5)/
    groupby(
      (Area/AreaPath),
      aggregate(StoryPoints with sum as StoryPoints)
    )
```


### **✔️ CONSIDER** structuring your query to match the OData evaluation order.
Previous section talked about the potential confusion caused by mixing `$apply` and `filter` clauses in a single query. In order to always make it clear you can structure your query to match the evaluation order.

1. `$apply`
2. `$filter`
3. `$orderby`
4. `$expand`
5. `$select`
6. `$skip`
7. `$top`


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
