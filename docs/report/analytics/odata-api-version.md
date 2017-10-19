---
title: OData API Versioning | VSTS  
description: How the Analytics service for Visual Studio Team Services (VSTS) manages changes to the OData API. 
ms.prod: vs-devops-alm
ms.technology: vs-devops-reporting
ms.assetid: BF30FE4E-0370-4C9B-A660-51207D816F8B
ms.manager: trevoc
ms.author: prprice
ms.date: 10/18/2017
---

# OData API Versioning
As the Analytics Service grows and changes we are dedicated to providing consistency and reliability to our users. To help meet these goals the Analytics Service provides a versioned OData api that users can trust will remain compatible with clients designed for those versions. Each version may be enhanced with additional functionaly and non-breaking changes. Incompatible or breaking changes will be rolled into future versions of the API.

The API version follows the _odata element in the request path and is formatted like **v1.0** or **v1.0-preview**.
```
https://{account}.analytics.visualstudio.com/{project}/_odata/{version}/$metadata
```


## Breaking vs non-breaking changes
The Data Model exposed by the Analytics Service defines the contract between the service and it's clients. The OData spec requires that clients be tolerant of additive changes but breaking changes will be introduced in future versions. For more information see the OData spec: http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part1-protocol/odata-v4.0-errata03-os-part1-protocol-complete.html#_Toc453752208

### Example of non-breaking changes
Consider a scenario where we add a new UserType property to the User entity.
```
<EntityType Name="User">
    <Key>
        <PropertyRef Name="UserSK"/>
    </Key>
    <Property Name="UserSK" Type="Edm.Guid" Nullable="false"/>
    <Property Name="UserId" Type="Edm.Guid" Nullable="false">
        <Annotation Term="Display.DisplayName" String="User Id"/>
    </Property>
    <Property Name="UserName" Type="Edm.String">
        <Annotation Term="Display.DisplayName" String="User Name"/>
    </Property>
    <Property Name="UserEmail" Type="Edm.String">
        <Annotation Term="Display.DisplayName" String="User Email"/>
    </Property>
    <Property Name="UserType" Type="Edm.Int32">
        <Annotation Term="Display.DisplayName" String="User Type"/>
    </Property>
</EntityType>
```
This change is additive and so could be made available in the current **V1.0** version.

### Example of breaking changes
Now consider a scenario where we reverted back to the original structure of the User entity.
```
<EntityType Name="User">
    <Key>
        <PropertyRef Name="UserSK"/>
    </Key>
    <Property Name="UserSK" Type="Edm.Guid" Nullable="false"/>
    <Property Name="UserId" Type="Edm.Guid" Nullable="false">
        <Annotation Term="Display.DisplayName" String="User Id"/>
    </Property>
    <Property Name="UserName" Type="Edm.String">
        <Annotation Term="Display.DisplayName" String="User Name"/>
    </Property>
    <Property Name="UserEmail" Type="Edm.String">
        <Annotation Term="Display.DisplayName" String="User Email"/>
    </Property>
</EntityType>
```
Since removal of the UserType field is a breaking change the field would not be removed until version **V2.0** of the API. **V1.0** of the data model would still include the UserType field.

## Version lifecycle
Each version of the OData API will go through three phases during it's lifecycle. 

### 1 - Preview
All breaking changes will be combined and released together in future versions of the API. In order to make this functionality available as early as possible we will release new versions in **preview** mode. While a version is in preview mode breaking changes are still possible, there are no guarantees that what is in preview will make it to the released version.

### 2 - Released
Once a preview version matures enough for release it will be made available without the -preview suffix. No breaking changes will be introduced to released versions but the data model may still grow with additive functionality. Released versions will be supported for a minimum of 12 months. The preview of a version will only be available for a few weeks after it is released, so it is important to migrate from the -preview to the released version quickly.

### 3 - Deprecated
Deprecated versions are no longer supported and requests made to them will not be fulfilled.

## Current preview versions
None

## Current supported versions
V1.0

## Current deprecated versions
None