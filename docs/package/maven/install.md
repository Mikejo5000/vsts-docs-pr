---
title: Install Maven packages from your feed using the Maven client
description: Successfully install Maven packages from Visual Studio Team Services or Team Foundation Server
ms.prod: vs-devops-alm
ms.technology: vs-devops-package
ms.topic: get-started-article
ms.assetid: 0f66e727-e76a-4a72-be12-3fa1775b9e2c
ms.manager: jenp
ms.author: rossav
ms.date: 04/05/2017
---

# Install Maven packages in Visual Studio Team Services and TFS

<!--
**Availability**<br>
Maven Package Management is available with **Visual Studio Team Services** and **TFS 2017 Update 3**.
-->

Install Maven packages from your feed using the Maven client.

1. [Set up the Maven client with your feed](./pom-and-settings.md).
2. Open a shell and navigate to the directory that contains your project's `POM.xml`.
3. Install a package by running `mvn install`. 

See the [Maven CLI docs](http://maven.apache.org/plugins/maven-install-plugin/usage.html) for more install options.