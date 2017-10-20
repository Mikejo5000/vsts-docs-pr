---
title: Data model for the Analytics Service for VSTS  
description: Describes the data entities and relationships provided by the Analytics service for Visual Studio Team Services (VSTS) 
ms.prod: vs-devops-alm
ms.technology: vs-devops-reporting
ms.assetid: 032FB76F-DC43-4863-AFC6-F8D67963B177  
ms.manager: douge
ms.author: kaelli
ms.date: 08/04/2017
---

# Data model for the Analytics Service  

**VSTS**  

[!INCLUDE [temp](../_shared/analytics-preview.md)]


The Analytics service data model consists of entities, each containing properties that can be filtered, aggregated, and summarized.  Additionally, entities contain [navigation properties](http://www.odata.org/getting-started/basic-tutorial/#relationship) that relate entities to each other, providing additional properties for filtering and grouping.

##Entities  

>[!NOTE]  
>The complete list of entities and properties varies for each VSTS project, and can be discovered by requestng the OData metadata: ```https://{account}.analytics.visualstudio.com/_odata/v1.0/$metadata```  

The data model contains the following entity sets:  

| EntitySet | Description|  
|--------|------------|  
|Areas | The work item area paths, with fields for grouping and filtering by area hierarchy |  
|Iterations | The work item iteration paths, with fields for grouping and filtering by iteration hierarchy |  
|BoardLocations | The Kanban board cell locations, as identified by board column, lane, and split - includes board settings|  
|Dates | The dates used to filter and group other entities using navigation or external joins|  
|Projects | All VSTS projects|  
|Tags | All work item tags for each project|  
|Teams | All VSTS teams|  
|Users | User information - used to expand or filter various work item fields (e.g. Assigned To, Created By)|  
|WorkItems | The current work items|  
|WorkItemLinks | The links between work items (e.g. child, parent, related) - includes history of links - hyperlinks not included  
|WorkItemRevisions | All work item revisions, including the current revision|  
|WorkItemSnapshot | (Composite) The state of each work item on each calendar date - a composite of WorkItemRevisions used for trend reporting|  
|WorkItemBoardSnapshot | (Composite) The state of each work item on each calendar date, including Kanban board location - a composite of WorkItemRevisions used for trend reporting|  
|WorkItemTypeFields | The work item fields for each work item type and process - used for report building|  

##Composite Entities

Some entities are composed from other simpler entities. Often these entities require more computing resources to generate and can sometimes return larger result sets. These composite entities are designed to specific scenarios, and care should be taken to query the correct entity for your query scenario, to ensure the best performance and avoid unnecessary throttling.

For example, WorkItemSnapshot combines WorkItemRevisions and Dates such that each date has one revision for each work item. This representation is useful for OData queries that want trend data for a filtered set of work items. However, this entity should not be used to query the current state of work items. Such a query would run more quickly using the WorkItem entity.

Similarly, some entities may contain all historic values, while others may only contain current values. WorkItemRevision contains all work item history, and should not be used in scenarios where the current values are of interest.

##Relationships

Entities can be combined using relationships to compute more complex query results. Within an OData query, relationships can be followed using navigation properties in the ```$expand```, ```$filter```, or ```groupby``` statements.

Some navigation properties result in a single entity, while others result in a collection of entities. In the following diagram, entities and their navigation properties are shown.  For clarity, some composite entities and relationships have been omitted.

![Analytics Service Data Model](_img/datamodel.png)

##Relationship Keys

 Entity relationships are also represented as foreign keys so that external tools can join entities. These fields have the suffix "SK", and are either integer or GUID data types. Date properties have corresponding integer date key properties with the following format: YYYYMMDD

##Entity Properties

The WorkItemRevision entity contains examples of different types of properties. Here is a sample:

| Property | Type | Description|  
|--------|------------|------------|  
|WorkItemRevisionSK | Int32 | The VSTS Analytics unique key for the work item revision - used by external tools to join related entities |  
|WorkItemId | Int32 | The VSTS id for the work item |  
|Revision | Int32 | The revision of the work item |  
|Title | String | The work item title |
|WorkItemType | String | The work item type (e.g. Bug, Task, User Story) |
|StoryPoints | Double | The points assign to this story - commonly aggregated as a sum
| Tags | Navigation | Navigation property to a Tag entity collection. Commonly used in ```$expand``` statements to access the Name property for multiple work item tags.
|CreatedDate | DateTimeOffset | The date the work item was created, expressed in the timezone for the account. Commonly used for filtering and for display.
|CreatedDateSK | Int32 | The date the work item was created, expressed as YYYYMMDD in the timezone for the account. Used by external tools to join related entities.
|CreatedOn | Navigation | Navigation property to the Date entity for the date the work item was created, in the timezone for the account. Commonly used to reference properties from the Date entity in ```groupby``` statements.

The last three properties here show how the same value is often expressed in multiple properties, each designed for different scenarios.


##Related notes 

- [WIT analytics](wit-analytics.md)  
- [Aggregate data](aggregated-data-analytics.md)
- [Overview of the analytics service](overview-analytics-service.md)


