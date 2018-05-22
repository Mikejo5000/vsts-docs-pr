---
title: Rate and service limits on public projects
titleSuffix: Azure Codex Public Project
description: Terms of service  
ms.technology: devops-agile
ms.prod: devops-alm
ms.topic: conceptual
ms.manager: douge
ms.author: kaelli
author: KathrynEE
ms.date: 06/02/2017
---

# Service limits 

[!INCLUDE [temp](_shared/version-public-projects.md)] 

Public projects are subject to the limits documented in this topic. 

 
## Codex Pipelines: Pipelines

TBD

## Codex Agile: Work items
- A long text field can contain 1M characters.
- You can't assign more than 100 tags to a work item.
- You can't add more than 1,000 links to a work item.
- You can't add more than 100 attachments to a work item.
- You can't add an attachment size larger than 60MB to a work item.


## Codex Agile: Custom work tracking 

Limits placed on the maximum number of custom work tracking objects that you can define for a public project are summarized below. You define these objects through an inheritance process. To learn more, see [Customize your work tracking process](../../settings/work/customize-process.md).

|Object | Inheritance | 
|-------|------------:|
| Work item types defined for a process | 64  |
| Fields defined for an account | 4096  | 
| Fields defined for a process | 512  | 
| Fields defined for a work item type | 512  |
| Pick lists defined for an account or collection | 512  | 
| Pick list items defined for a list | 512  | 
| Pick list item character length | 256  | 
| Workflow states defined for a work item type | 32  |
| Rules defined for a work item type | 1024  |
| Portfolio backlog levels defined for a process| 5  |

 
## Wiki

Wikis defined for a team project are limited to 1 GB per git repository.  