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

# Data model for the Analytics service  

**VSTS**  

[!INCLUDE [temp](../_shared/analytics-preview.md)]


The Analytics service data model consists of data entities, each containing properties than can be filtered, aggregated, and summarized.  Additionally, entities contain navigation properties that relate entities to each other, providing additional properties for filtering and grouping.

##Entities  

>[!NOTE]  
>The complete list of entities and properties varies for each VSTS project, and can be discovered by requestng the OData metadata: ```https://{account}.analytics.visualstudio.com/_odata/v1.0/$metadata```.  

The data model contains the following entity sets:  

| EntitySet | Description|  
|--------|------------|  
|Areas | The work item area paths, with fields for grouping and filtering by area hierarchy |  
|Iterations | The work item iteration paths, with fields for grouping and filtering by iteration hierarchy |  
|BoardLocations | The Kanban board locations, as identified by board column, lane, and split |  
|Dates | The dates used to filter and group other entities using navigation or external joins|  
|Projects | All VSTS projects|  
|Tags | All work item tags for each project|  
|Teams | All VSTS teams|  
|Users | User information - used to expand or filter various work item fields (e.g. Assigned To, Created By)|  
|WorkItems | The current work items|  
|WorkItemLinks | The links between work items (e.g. child, parent, related) - includes history of links - hyperlinks not included  
|WorkItemRevisions | All work item revisions, including the current revision|  
|WorkItemSnapshot | The state of each work item on each calendar date - a derivitive of WorkItemRevisions used for trend reporting|  
|WorkItemBoardSnapshot | The state of each work item on each calendar date, including Kanban board location - a derivitive of WorkItemRevisions used for trend reporting|  
|WorkItemTypeFields | The work item fields for each work item type and process - used for report building|  

##Relationships

Entities can be combined using relationships to compute more complex query results. Within an OData query, relationships can be followed using navigation properties in the expand, filter, or groupby statements.

Some navigation properties result in a single entity, while others result in sets of entities. In the following diagram, entities and their navigation properties are shown.  For clarity, some derivitive entities and relationships have been omitted.

![Analytics Service Data Model](_img/datamodel.png)

##Relationship Keys

 Entity relationships are also exposed as foreign keys so that external tools can implement joins. These fields have the suffix "SK", and are either integer or GUID data types. Date properties will have corresponding integer date key properties that use the following format: YYYYMMDD

##Entity properties

The WorkItemRevision entity has examples of both types of properties. Here is a sample:

| Property | Type | Description|  
|--------|------------|------------|  
|WorkItemRevisionSK | Int32 | The VSTS Analytics unique key for the work item revision. Used by external tools to join related entities. |  
|WorkItemId | Int32 | The VSTS id for the work item |  
|Revision | Int32 | The revision of the work item |  
|Title | String | The work item title |
|WorkItemType | String | The work item type (e.g. Bug, Task, User Story) |
|StoryPoints | Double | The points assign to this story. Commonly aggregated as a sum.
| Tags | Navigation | Navigation property to a Tag entity collection. Commonly used in expand statements to access the Name property for multiple work item tags.
|CreatedDate | DateTimeOffset | The date the work item was created, expressed in the timezone for the account. Commonly used for filtering and for display.
|CreatedDateSK | Int32 | The date the work item was created, expressed as YYYYMMDD in the timezone for the account. Used by external tools to join related entities.
|CreatedOn | Navigation | Navigation property to the Date entity for the date the work item was created, in the timezone for the account. Commonly used to reference properties from the Date entity in groupby statements.

The last three properties here show how the same value is often expressed in multiple properties, each designed for different scenarios.





##Related notes 

- [WIT analytics](wit-analytics.md)  
- [Aggregate data](aggregated-data-analytics.md)
- [Overview of the analytics service](overview-analytics-service.md)


