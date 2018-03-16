---
title: Migration checklist
titleSuffix: Azure CodeX Public Project 
description: Best practices when changing a private project to a public project 
ms.technology: vs-devops-wit
ms.prod: vs-devops-alm
ms.assetid: 
ms.manager: douge
ms.author: kaelli
ms.topic: get-started-article
ms.date: 01/05/2018
---

# Migration checklist

[!INCLUDE [temp](_shared/version-public-projects.md)] 

Most existing team projects contain a large amount of historical data.
Old work items, early commits, and previous build definitions might have content you aren't comfortable sharing publicly.
This checklist contains a list of things to think about before making a project public.
Also, it has ideas for migrating the latest state to a new project so that you can expose only current and future content.

## Checklist

| **Area**   | **Considerations** |
|------------|---|
| Agile      | |
|------------|---|
| Code       | |
|------------|---|
| CI/CD      | |
|------------|---|
| Testing    | |
|------------|---|
| Reporting  | |
|------------|---|
| Extensions | |

## Tips for migrating a subset

- Migrate just the tip of all Git repos, after ensuring nothing undesirable exists there 
- Copy any important bugs (maybe with the new WIMigrator tool?)
- Export and import build definitions 
 