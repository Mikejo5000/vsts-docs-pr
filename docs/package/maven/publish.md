---
title: Publish Maven packages to your feed using the Maven client
description: Successfully publish Maven packages to your feed hosted on Visual Studio Team Services or Team Foundation Server
ms.prod: vs-devops-alm
ms.technology: vs-devops-package
ms.topic: get-started-article
ms.assetid: 9b2c7b3d-32d0-4ce1-8e17-ec9e8c3e451f
ms.manager: jenp
ms.author: rossav
ms.date: 04/05/2017
---

# Publish Maven packages in Visual Studio Team Services and TFS

<!--
**Availability**<br>
Maven Package Management is available with **Visual Studio Team Services** and **TFS 2017 Update 3**.
-->

Publish Maven packages to a feed in Package Management to share them with your team and your organization.

1. [Set up the Maven client with your feed](./pom-and-settings.md).
2. Open a shell and navigate to the directory that contains your package's `POM.xml`.
If you don't have a `POM.xml`, run `mvn archetype:generate` ([see the Maven CLI docs](https://maven.apache.org/guides/getting-started/index.html#How_do_I_make_my_first_Maven_project)).
3. Push your package by running `mvn deploy` inside the directory containing your POM.xml.

See the [Maven CLI docs](http://maven.apache.org/plugins/maven-deploy-plugin/) for more publish options.