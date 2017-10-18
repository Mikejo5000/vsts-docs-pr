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
Problem statement/why we version.

## Breaking vs non-breaking changes
Contract with clients changes only for breaking changes like renames, deletions. OData spec is tolerant of non-breaking changes like additions.

### Examples of breaking changes
Metadata before -> metadata after

### Examples of non-breaking changes
Metadata before -> metadata after

## Requesting an unsupported version
Request/response examples for invalid/unsupported versions.

### Example: Request deprecated version
### Example: Request preview version of released version
### Example: Request invalid version

## Version lifecycle
Preview -> released -> deprecated

### Preview
Set expectations. Breaking changes. No guarantees.

### Released
Preview version no longer available.
Non-breaking changes only. Commited to support for 12 months.
Some overlap between Preview and Released.

### Deprecated
Version no longer supported. Requests will be rejected. What does communication look like before we "pull the plug".

## Current preview versions
None

## Current supported versions
V1.0, not mentioning V1.0-Preview

## Current deprecated versions
None