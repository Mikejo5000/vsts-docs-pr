---
title: YAML build definitions | VSTS & TFS    
description: Learn how to use YAML to configure CI/CD for the app and platform of your choice.
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: 7d7d49ec-7e60-42a1-8d9f-c77eb7181373
ms.manager: douge
ms.author: alewis
author: ericsciple
ms.reviewer: macoope
ms.date: 07/17/2018
ms.topic: reference
monikerRange: '>= tfs-2018'
---

# YAML build definitions

To create a YAML build definition, you must opt-in to the account-level preview feature: `Build YAML definitions`

YAML builds require the latest agent. When a YAML build is queued, your agent will automatically update if it is not the latest version.

## Basics

[Create a definition](definition.md)

[Pipeline overview](pipeline.md)

[Pipeline instance name](name.md)

## Scripts and tasks

[Run scripts](scripts.md)

[Run powershell scripts](powershell.md)

[Run bash scripts](bash.md)

[Checkout repositories](checkout.md)

[Run tasks](tasks.md)

## Triggers

[Continuous integration](ci.md)

## Variables

[Predefined variables](https://docs.microsoft.com/en-us/vsts/pipelines/build/variables)

[Macro syntax](macros.md)

[Accessing variables from scripts](accessingvariables.md)

[Custom variables](customvariables.md)

[Setting variables from a script](setvariable.md)

[Secret variables](secretvariables.md)

[Output variables](outputvariables.md)

[OAuth token for scripts](token.md)

## Resources

[Authorization](authz.md)

[Endpoints](endpoints.md)

[Secure files](securefiles.md)

<!-- todo: [Variable groups](variablegroups.md) -->

## Phases

[Options](job.md)

[Pools](pools.md)

[Containers](containers.md)

[Matrix execution](matrix.md)

[Slice execution](slice.md)

[Multiple phases](jobs.md)

[Output variables](outputvariables.md)

## Templates

[Step reuse](reusestep.md)

[Phase reuse](reusephase.md)

[Reuse from other repositories](reusefromrepo.md)

[Template expressions](templateexpressions.md)

## Schema reference

[Schema reference](schema.md)

<!-- todo: [Escaping](escaping.md) -->
