---
title: Create a definition | VSTS & TFS    
description: Learn how to use YAML to configure CI/CD for the app and platform of your choice.
ms.prod: devops
ms.technology: devops-cicd
ms.assetid: 3c1f8df4-0ac6-47e5-8c95-928edb6dd1da
ms.manager: douge
ms.author: alewis
author: ericsciple
ms.reviewer: macoope
ms.date: 07/17/2018
ms.topic: reference
monikerRange: '>= tfs-2018'
---

# Create a definition

## When using a Git repo in your VSTS team project

Push a YAML file `.vsts-ci.yml` to the root directory of your repository. A definition
`<REPO_NAME>/<REPO_NAME> CI` will be created, and a CI build will be triggered.

Note, the definition will only be created if whoever pushes the branch update has
permission to create a definition.

Optionally a new YAML definition can be created from the web UI. You can choose any YAML
file within your repository.

## When using a Git repo in GitHub

A new YAML definition can be created from the web UI. You can choose any YAML file within
your repository.

## Hello world

Use the below YAML content to run a job that prints hello world!

```yaml
queue: Hosted VS2017

steps:
- script: echo hello world
```
