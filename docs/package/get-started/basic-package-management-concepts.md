---
title: Azure DevOps XXX New User Guide - Key Concepts
description: Learn about key concepts and components for XXX in Visual Studio Team Services (VSTS) and Team Foundation Server (TFS)
ms.prod: devops
ms.technology: devops-artifacts
ms.manager: douge
ms.author: elbatk
author: elbatk
ms.reviewer: amullans
ms.date: 01/31/2018
monikerRange: '>= tfs-2017'
---

# Key Concepts for Azure DevOps XXX Users 

Learn about the key concepts and components that are used in XXX. Understanding the basic terms and parts of XXX will help you further explore how it can help you...?

## How XXX works

> **elbatk:** Diagram/image here that can easily explain the flow of package management.

## Key terms

### What are 'feeds'?

Package Management organizes packages into *feeds* - what the NuGet client calls ''package sources''. Feeds make it simple to set permissions for and organize groups of packages. 

### What are 'views'?

Views enable you to share subsets of the package-versions in your feed with consumers. 

A common use for views is to share package-versions that have been tested, validated, or deployed but hold back packages still under development and packages that didn't meet a quality bar.

### What are 'upstream sources'?

Upstream sources enable you to use a single feed to store both the packages you produce and the packages you consume from "remote feeds": both public feeds (e.g. npmjs.com and nuget.org) and authenticated feeds (i.e. other VSTS feeds in your account or organization). Once you've enabled an upstream source, any user connected to your feed can install a package from the remote feed, and your feed will save a copy.

### What are 'complete graphs'?

When you release a package, it's important to ensure that any dependencies of that package are also available in your feed, either by republishing them directly (not recommended) or by consuming them from an [upstream source](../concepts/upstream-sources.md). Once you consume a package from an upstream source once, a copy of it is always saved in your feed. Even if the upstream source goes down, your copy will remain available both to you and to your downstream consumers.

### What are 'symbols'?

To debug compiled executables, especially executables compiled from native code languages like C++, you need symbol files that contain debugging information. These files generally have the PDB (program database) extension. 

## What's in a symbol file
Symbols contain a set of useful debugging information, including:
- publics and exports
- global symbols
- local symbols
- type data
- source indexes
- line numbers

### What is 'immutability'?

Once you publish a particular version of a package to a feed, that version number is permanently reserved. 
You cannot upload a newer revision package with that same version number, or delete it and upload a new package at the same version.



