---
title: Linked work item queries | VSTS  
description: How to query for linked work items using the Analytics service for Visual Studio Team Services (VSTS)  
ms.prod: vs-devops-alm
ms.technology: vs-devops-reporting
ms.assetid: BF30FE4E-0370-4C9B-A660-51207D816F8B
ms.manager: douge
ms.author: kaelli
ms.date: 08/11/2016
---

#Query for linked work items 

**VSTS**  

Querying work items across links is similar to any other operation across related entities in OData, but because links are entities with their own properties there is some additional complexity.

There are two ways to query for linked items. The first is the Parent/Child hierarchy, the second is the Links navigation property. The sections below cover each approach.

## Parent/Child hierarchy
Items that are linked together with Parent/Child links can be included in query results by using $expand on the Parent and Children properties.

### Example: Parent to child query
To return information about a particular item's children use $expand on the **Children** navigation property.

Request
```
https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/WorkItems?$select=WorkItemId,Title,State&$expand=Children($select=WorkItemId,Title,State)&$filter=WorkItemId eq [ID #]
```

Response
```
{
  "@odata.context":"https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/$metadata#WorkItems(WorkItemId,Title,State,Children,Children(WorkItemId,Title,State))","value":[
    {
      "WorkItemId":103,"Title":"Feature Y","State":"New","Children":[
        {
          "WorkItemId":48,"Title":"Story 15","State":"Resolved"
        },{
          "WorkItemId":50,"Title":"Story 17","State":"New"
        },{
          "WorkItemId":55,"Title":"Story 22","State":"New"
        }
      ]
    }
  ]
}
```

### Example: Multiple levels of hierarchy
Users may be interested in all descendants of a particular set of work items in which case the **$levels** option can be used. The **$levels** option allows the user to control how many levels deep the service will traverse when retrieving items. In this example **max** actually equates to $levels=5 but users may substitute other values.

**Note:** The $levels option only works for recursive relationships.

Request
```
https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/WorkItems?$select=WorkItemId,Title,State&$expand=Children($select=WorkItemId,Title,State;$levels=max)&$filter=WorkItemId eq 103
```

Response
```
{
  "@odata.context":"https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/$metadata#WorkItems(WorkItemId,Title,State,Children,Children(WorkItemId,Title,State,Children,Children(WorkItemId,Title,State)))","value":[
    {
      "WorkItemId":103,"Title":"Feature Y","State":"New","Children":[
        {
          "WorkItemId":48,"Title":"Story 15","State":"Resolved","Children":[
            {
              "WorkItemId":104,"Title":"Task A","State":"New"
            }
          ]
        },{
          "WorkItemId":50,"Title":"Story 17","State":"New","Children":[]
        },{
          "WorkItemId":55,"Title":"Story 22","State":"New","Children":[
            {
              "WorkItemId":105,"Title":"Task B","State":"New"
            }
          ]
        }
      ]
    }
  ]
}

```

Notice that the "Story 15" and "Story 22" items now include their child items.

### Example: Child to parent query

By replacing **Children** with **Parent** in the $expand option users can retrieve an item's ancestry.

Request
```
https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/WorkItems?$select=WorkItemId,Title,State&$expand=Parent($select=WorkItemId,Title,State;$levels=max)&$filter=WorkItemId eq 105
```

Response
```
{
  "@odata.context":"https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/$metadata#WorkItems(WorkItemId,Title,State,Parent,Parent(WorkItemId,Title,State,Parent,Parent(WorkItemId,Title,State)))","value":[
    {
      "WorkItemId":105,"Title":"Task B","State":"New","Parent":{
        "WorkItemId":55,"Title":"Story 22","State":"New","Parent":{
          "WorkItemId":103,"Title":"Feature Y","State":"New"
        }
      }
    }
  ]
}
```

## Non-hierarchical links
In addition to the Parent/Child hierarchy items can be directly related to other items with link types like *Related* or *Duplicate*. The **Links** navigation property allows users to request these relationships.

### Example: Request an item's links
Users interested in the links associated with an item may $expand the **Links** navigation property.

Request
```
https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/WorkItems?$select=WorkItemId,Title,WorkItemType,State&$filter=WorkItemId%20eq%20103&$expand=Links
```

Response
```
{
  "@odata.context":"https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/$metadata#WorkItems(WorkItemId,Title,WorkItemType,State,Links)","value":[
    {
      "WorkItemId":103,"Title":"Feature Y","WorkItemType":"Feature","State":"New","Links":[
        {
          "SourceWorkItemId":103,"TargetWorkItemId":48,"CreatedDate":"2016-01-14T16:30:56.287Z","DeletedDate":null,"Comment":"","LinkTypeId":2,"LinkTypeReferenceName":"System.LinkTypes.Hierarchy-Forward","LinkTypeName":"Child","LinkTypeIsAcyclic":true,"LinkTypeIsDirectional":true
        },{
          "SourceWorkItemId":103,"TargetWorkItemId":50,"CreatedDate":"2016-01-14T16:30:50.277Z","DeletedDate":null,"Comment":"","LinkTypeId":2,"LinkTypeReferenceName":"System.LinkTypes.Hierarchy-Forward","LinkTypeName":"Child","LinkTypeIsAcyclic":true,"LinkTypeIsDirectional":true
        },{
          "SourceWorkItemId":103,"TargetWorkItemId":55,"CreatedDate":"2016-01-14T16:30:53.867Z","DeletedDate":null,"Comment":"","LinkTypeId":2,"LinkTypeReferenceName":"System.LinkTypes.Hierarchy-Forward","LinkTypeName":"Child","LinkTypeIsAcyclic":true,"LinkTypeIsDirectional":true
        },{
          "SourceWorkItemId":103,"TargetWorkItemId":112,"CreatedDate":"2016-03-03T17:17:46.023Z","DeletedDate":null,"Comment":"","LinkTypeId":1,"LinkTypeReferenceName":"System.LinkTypes.Related-Forward","LinkTypeName":"Related","LinkTypeIsAcyclic":false,"LinkTypeIsDirectional":false
        }
      ]
    }
  ]
}
```
### Example: Request details of linked items
The previous query only retreives details on the links between items. A user may include the details of those linked items by using $expand on the **TargetWorkItem** navigation property of the link.

Request
```
https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/WorkItems?$select=WorkItemId,Title,WorkItemType,State&$filter=WorkItemId%20eq%20103&$expand=Links($expand=TargetWorkItem($select=WorkItemId,Title,State))
```

Response
```
{
  "@odata.context":"https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/$metadata#WorkItems(WorkItemId,Title,WorkItemType,State,Links,Links(TargetWorkItem(WorkItemId,Title,State)))","value":[
    {
      "WorkItemId":103,"Title":"Feature Y","WorkItemType":"Feature","State":"New","Links":[
        {
          "SourceWorkItemId":103,"TargetWorkItemId":48,"CreatedDate":"2016-01-14T16:30:56.287Z","DeletedDate":null,"Comment":"","LinkTypeId":2,"LinkTypeReferenceName":"System.LinkTypes.Hierarchy-Forward","LinkTypeName":"Child","LinkTypeIsAcyclic":true,"LinkTypeIsDirectional":true,"TargetWorkItem":{
            "WorkItemId":48,"Title":"Story 15","State":"Resolved"
          }
        },{
          "SourceWorkItemId":103,"TargetWorkItemId":50,"CreatedDate":"2016-01-14T16:30:50.277Z","DeletedDate":null,"Comment":"","LinkTypeId":2,"LinkTypeReferenceName":"System.LinkTypes.Hierarchy-Forward","LinkTypeName":"Child","LinkTypeIsAcyclic":true,"LinkTypeIsDirectional":true,"TargetWorkItem":{
            "WorkItemId":50,"Title":"Story 17","State":"Active"
          }
        },{
          "SourceWorkItemId":103,"TargetWorkItemId":55,"CreatedDate":"2016-01-14T16:30:53.867Z","DeletedDate":null,"Comment":"","LinkTypeId":2,"LinkTypeReferenceName":"System.LinkTypes.Hierarchy-Forward","LinkTypeName":"Child","LinkTypeIsAcyclic":true,"LinkTypeIsDirectional":true,"TargetWorkItem":{
            "WorkItemId":55,"Title":"Story 22","State":"New"
          }
        },{
          "SourceWorkItemId":103,"TargetWorkItemId":112,"CreatedDate":"2016-03-03T17:17:46.023Z","DeletedDate":null,"Comment":"","LinkTypeId":1,"LinkTypeReferenceName":"System.LinkTypes.Related-Forward","LinkTypeName":"Related","LinkTypeIsAcyclic":false,"LinkTypeIsDirectional":false,"TargetWorkItem":{
            "WorkItemId":112,"Title":"Some issue","State":"Active"
          }
        }
      ]
    }
  ]
}
```

### Example: Links of a specific type
Users may be interested in a particular type of link between items, in which case the **LinkTypeName** property can be used in a $filter.

Request
```
https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/WorkItems?$select=WorkItemId,Title,WorkItemType,State&$filter=WorkItemId%20eq%20103&$expand=Links($filter=LinkTypeName eq 'Related';$expand=TargetWorkItem($select=WorkItemId,Title,State))
```

Response
```
{
  "@odata.context":"https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/$metadata#WorkItems(WorkItemId,Title,WorkItemType,State,Links,Links(TargetWorkItem(WorkItemId,Title,State)))","value":[
    {
      "WorkItemId":103,"Title":"Feature Y","WorkItemType":"Feature","State":"New","Links":[
        {
          "SourceWorkItemId":103,"TargetWorkItemId":112,"CreatedDate":"2016-03-03T17:17:46.023Z","DeletedDate":null,"Comment":"","LinkTypeId":1,"LinkTypeReferenceName":"System.LinkTypes.Related-Forward","LinkTypeName":"Related","LinkTypeIsAcyclic":false,"LinkTypeIsDirectional":false,"TargetWorkItem":{
            "WorkItemId":112,"Title":"Some issue","State":"Active"
          }
        }
      ]
    }
  ]
}
```