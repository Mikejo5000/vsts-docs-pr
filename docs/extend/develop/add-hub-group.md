---
ms.prod: devops
ms.technology: devops-ecosystem
title: Add a Hub Group | Extensions for VSTS
description: Add a hub group in VSTS for your extension.
ms.assetid: 8186f578-27a0-4130-ace0-0279c863b1a5
ms.topic: conceptual
ms.manager: douge
monikerRange: '>= tfs-2017'
ms.author: elbatk
author: elbatk
ms.date: 08/04/2016
---

# Add a hub group

We'll create a hub group and add hub to it.
If you haven't already, [create the Hello hub](./add-hub.md) first,
then follow these steps to create the hub group.

[!INCLUDE [Hub_group](../_shared/procedures/create-hub-group.md)]

Here's the complete extension manifest with Hello in the samples hub group.

	```json
	{
		"id": "MyExtension",
		"publisher": "Fabrikam",
		"name": "My Extension",
		"description": "This is my first extension",
		"version": "1.0",
		"contributions": [
            {
                "id": "sample-hub-group",
                "type": "ms.vss-web.hub-group",
                "targets": [
                    "ms.vss-web.project-hub-groups-collection"
                ],
                "properties": {
                    "name": "Samples",
                    "order": 100
                }
            },
			{
                "id": "sample-hub",
                "type": "ms.vss-web.hub",
                "targets": [
                    ".sample-hub-group"
                ],
                "properties": {
                    "name": "Hello",
                    "order": 99,
                    "uri": "hello-world.html"
                }
            }
		]
	}
	```