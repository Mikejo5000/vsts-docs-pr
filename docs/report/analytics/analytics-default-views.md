---
title: Default Analytics Views
titleSuffix: VSTS
description: Default Analytics Views that are automatically created when installing the VSTS Analytics extension 
ms.prod: vs-devops-alm
ms.technology: vs-devops-reporting
ms.assetid: 
ms.reviewer: greggboe
ms.manager: douge
ms.author: kaelli
ms.date: 2/8/2018
---

# Default Analytics Views

**VSTS**  

For information on Analytics Views, read [What are Analytics Views](./what-are-analytics-views.md)

When you install the [VSTS Analytics extension](https://marketplace.visualstudio.com/items?itemName=ms.vss-analytics), we create a set of default Analytics Views. These views are immediately available from Power BI and are a great way to get started.

![VSTS Power BI Integration - Data Connector - Default Analytics Views](./_img/data-connector-views-default.png)

The default Analytics Views provided are a combination of options for Work Item Types and Historical data returned. The following tables describe each set of options.

## Options for work item types

| Work item type option | Description |
|-|-|
| Work Items | Load current or historical state of all Work Items  |
| Bugs | Load current or historical state of Bugs only |

## Options for Historical data

| Historical option | Description |
|-|-|
| Today | Loads only the most recent revision for each work item. |
| Last 30 days | Loads work item history for the last 30 days, on a daily interval.
| Last 26 weeks | Loads work item history for the last 26 weeks, on a weekly interval.
| All history by month | Loads all work item history, on a monthly interval

## Fields returned in default Analytics Views
Default views will automatically return the most common reportable fields for the included work item types. All custom fields are included. Date fields used for auditing, such as Created Date, Activated Date, and Closed Date are not included, as they often cause confusion with trend reporting.

## When Default Views aren't enough
The default Analytics Views return all the specified data in a VSTS team project. They work well for customers with smaller accounts. With larger accounts, the amount of data may be simply too much for Power BI to load.

**If the default Analytics Views do not meet your needs**, you can create your customized Analytics Views to fine-tune the records, fields, and history returned to Power BI.

For more information on creating custom Analytics Views, read [Create & manage Analytics views](analytics-views-create.md).