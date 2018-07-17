---
title: Pipeline overview | VSTS & TFS    
description: Learn how to use YAML to configure CI/CD for the app and platform of your choice.
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: 4e782159-ca47-43ae-bd38-36cec8de3e0d
ms.manager: douge
ms.author: alewis
author: ericsciple
ms.reviewer: macoope
ms.date: 07/17/2018
ms.topic: reference
monikerRange: '>= tfs-2018'
---

# Pipeline overview

## Pipeline

A pipeline contains phases. Phases contain steps.

```
-----------------------------------
|            Pipeline             |
|                                 |
|    -------------------------    |
|    |        Phases         |    |
|    |                       |    |
|    |    ---------------    |    |
|    |    |    Steps    |    |    |
|    |    ---------------    |    |
|    |                       |    |
|    -------------------------    |
|                                 |
-----------------------------------
```

<!-- A pipeline contains stages. Stages contain jobs. Jobs contain steps.

```
---------------------------------------------
|                 Pipeline                  |
|                                           |
|    -----------------------------------    |
|    |             Stages              |    |
|    |                                 |    |
|    |    -------------------------    |    |
|    |    |         Jobs          |    |    |
|    |    |                       |    |    |
|    |    |    ---------------    |    |    |
|    |    |    |    Steps    |    |    |    |
|    |    |    ---------------    |    |    |
|    |    |                       |    |    |
|    |    -------------------------    |    |
|    |                                 |    |
|    -----------------------------------    |
|                                           |
---------------------------------------------
```

## Stages

Stages provide a logical boundary within the pipeline.

The stage boundary allows:
- Manual checkpoints or approvals between stages
- Reporting on high level results (email notifications, build badges) -->

## Phases

A phase is a group of steps, and is assigned to a specific target.

For example, when a phase targets an agent pool, the phase will be assigned to one of the agents running within the pool.

## Steps

Steps are the individual units of execution within a phase. For example, run a script.
