---
title: Exploring Analytics OData metadata | VSTS  
description: Guidance on how to explore Analytics metadata in Visual Studio Team Services (VSTS). 
ms.prod: vs-devops-alm
ms.technology: vs-devops-reporting
ms.assetid: BF30FE4E-0370-4C9B-A660-51207D816F8B
ms.manager: greggboe
ms.author: jozimm
ms.date: 10/20/2017
---

# Exploring Analytics OData metadata

**VSTS**

[!INCLUDE [temp](../_shared/analytics-preview.md)]

In this topic you'll learn how to:
>[!div class="checklist"]

>* Query the metadata on a specific team project
>* Query the metadata on a Account
>* Identify the keys, properties, and navigational properties associated with an Entity
>* Identify the capabilities of the Analytics OData endpoint

This introductory tutorial provides guidance for exploring Analytics metadata.  [OData metadata](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part3-csdl/odata-v4.0-errata03-os-part3-csdl-complete.html#_Toc453752662) is a machine readable description of the entity model designed to enable client consumption. Understanding the metadata associated with the entity model is a pre-requisite for programmatically querying the [Analytics OData v4 endpoint](data-model-analytics-service.md).

## How to query the service for metadata
Analytics exposes the [entity model](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part3-csdl/odata-v4.0-errata03-os-part3-csdl-complete.html#_Toc453752500) at the metadata URL, formed by appending $metadata to the service root URL. Analytics provides service roots for the [Projects or entire Account](account-scoped-queries.md).


### Query for metadata on a specific team project
You construct the service root URL for a team project as shown:

```
https://{account}.analytics.visualstudio.com/{project}/_odata/v1.0/$metadata
```


### Query for metadata on a Account
The service root URL at the Account level is constructed as:

```
https://{account}.analytics.visualstudio.com/_odata/v1.0/$metadata
```

# Interpret the metadata response
The core components of the metadata response are EntityType and EntityContainer.

```XML
<?xml version="1.0" encoding="UTF-8"?>
<edmx:Edmx xmlns:edmx="http://docs.oasis-open.org/odata/ns/edmx" Version="4.0">
    <edmx:DataServices>
        <Schema xmlns="http://docs.oasis-open.org/odata/ns/edm" Namespace="Microsoft.VisualStudio.Services.Analytics.Model">
           <EntityType Name="Entity Name"/>
        </Schema>
        <Schema xmlns="http://docs.oasis-open.org/odata/ns/edm" Namespace="Default">
           <EntityContainer Name="Container"/>
        </Schema>
    </edmx:DataServices>
</edmx:Edmx>
```

## EntityTypes
EntityTypes define each of the Entities in the model including properties and relationships. 

```XML
<EntityType Name="Project">
   <Key>
      <PropertyRef Name="ProjectSK"/>
   </Key>
   <Property Name="ProjectSK" Nullable="false" Type="Edm.Guid"/>
   <Property Name="ProjectId" Nullable="false" Type="Edm.Guid">
      <Annotation String="Project Id" Term="Display.DisplayName"/>
   </Property>
   <Property Name="ProjectName" Nullable="false" Type="Edm.String">
      <Annotation String="Project Name" Term="Display.DisplayName"/>
   </Property>
   <NavigationProperty Name="Areas" Type="Collection(Microsoft.VisualStudio.Services.Analytics.Model.Area)"/>
   <NavigationProperty Name="Iterations" Type="Collection(Microsoft.VisualStudio.Services.Analytics.Model.Iteration)"/>
   <NavigationProperty Name="Teams" Type="Collection(Microsoft.VisualStudio.Services.Analytics.Model.Team)"/>
</EntityType>
```

### Keys
Keys define the Entity properties available for use as a Navigational Property.

```XML
<Key>
   <PropertyRef Name="ProjectSK"/>
</Key>
```

### Properties
The set of Entity properties available for query. Annotations represent additional details about a given property. 

Any property of Analytics that should be visible to end users is annotated with a DisplayName.

```XML
<Property Name="ProjectSK" Nullable="false" Type="Edm.Guid"/>
<Property Name="ProjectId" Nullable="false" Type="Edm.Guid">
   <Annotation String="Project Id" Term="Display.DisplayName"/>
</Property>
<Property Name="ProjectName" Nullable="false" Type="Edm.String">
   <Annotation String="Project Name" Term="Display.DisplayName"/>
</Property>
```

ReferenceName is another common annotation used to define the system identifier for a specific property.

```XML
<Property Name="State" Type="Edm.String">
   <Annotation String="State" Term="Display.DisplayName"/>
   <Annotation String="System.State" Term="Ref.ReferenceName"/>
</Property>
```

### Navigational Properties
Querying an individual Entity is useful, but eventually you will want to be able to filter or expand details of another Entity. To do this, you need to understand how to use the [Navigational Properties](data-model-analytics-service.md) of the Entity model. 

A Navigational Property with a Collection type represents a many to many relationship in the model.

```XML
<NavigationProperty Name="Teams" Type="Collection(Microsoft.VisualStudio.Services.Analytics.Model.Team)"/>
```

ReferentialConstraints tie Navigational Properties to a specific key of an Entity, represeting a many to one relationship in the model.

```XML
<NavigationProperty Name="Project" Type="Microsoft.VisualStudio.Services.Analytics.Model.Project">
   <ReferentialConstraint ReferencedProperty="ProjectSK" Property="ProjectSK"/>
</NavigationProperty>
```

## Container (OData capabilities)

### EntitySets
EntitySets represents a collection of entities and associated Navigational Property Bindings and Annotations.

```XML
<EntitySet Name="Projects" EntityType="Microsoft.VisualStudio.Services.Analytics.Model.Project">
   <NavigationPropertyBinding Target="Teams" Path="Teams"/>
   <Annotation String="Projects" Term="Org.OData.Display.V1.DisplayName"/>
</EntitySet>
```

### Capabilities
Capabilities and Aggregation annotations define the set of [functions](../extend-analytics/odata-supported-features) understood by the Analytics OData endpoint.

```XML
<Annotation Term="Org.OData.Capabilities.V1.FilterFunctions">
   <Collection>
      <String>contains</String>
      <String>endswith</String>
      <String>startswith</String>
      <String>length</String>
      <String>indexof</String>
      <String>substring</String>
      <String>tolower</String>
      <String>toupper</String>
      <String>trim</String>
      <String>concat</String>
      <String>year</String>
      <String>month</String>
      <String>day</String>
      <String>hour</String>
      <String>minute</String>
      <String>second</String>
      <String>fractionalseconds</String>
      <String>round</String>
      <String>floor</String>
      <String>ceiling</String>
      <String>date</String>
      <String>time</String>
      <String>isof</String>
      <String>cast</String>
   </Collection>
</Annotation>
```

```XML
<Annotation Term="Org.OData.Aggregation.V1.ApplySupported">
   <Record>
      <PropertyValue Property="Transformations">
         <Collection>
            <String>aggregate</String>
            <String>filter</String>
            <String>groupby</String>
         </Collection>
      </PropertyValue>
   </Record>
</Annotation>
```

```XML
<Annotation Term="Org.OData.Capabilities.V1.BatchSupportType" Bool="true"/>
<Annotation Term="Org.OData.Capabilities.V1.BatchSupportType">
   <Record>
      <PropertyValue Property="Supported" Bool="true"/>
      <PropertyValue Property="ContinueOnErrorSupported" Bool="false"/>
      <PropertyValue Property="ReferencesInRequestBodiesSupported" Bool="false"/>
      <PropertyValue Property="ReferencesAcrossChangeSetsSupported" Bool="false"/>
      <PropertyValue Property="EtagReferencesSupported" Bool="false"/>
   </Record>
</Annotation>
```