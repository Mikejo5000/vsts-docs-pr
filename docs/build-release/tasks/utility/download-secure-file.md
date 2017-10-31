---
title: Download Secure File
description: Download a secure file to a temporary location on the build or release agent
ms.prod: vs-devops-alm
ms.technology: vs-devops-build
ms.assetid: 2a6ca863-f2ce-4f4d-8bcb-15e64608ec4b
ms.manager: taylaf
ms.author: madhurig
ms.date: 10/31/2017
---

# Utility: Download Secure File

**VSTS**

![](../utility/_img/secure-file.png) Download a secure file to a temporary location on the build or release agent

This task allows downloading a file that is stored as a [secure file](../../concepts/library/secure-files.md) on the server during a build or release.

## Agent version

2.116.0 or higher is required

## Arguments

| Argument | Description |
| -------- | ----------- |
| Secure File | Select the secure file to download to a temporary location on the agent. The file will be cleaned up after the build or release. |
