---
title: Performance and Latency | VSTS  
description: S 
ms.prod: vs-devops-alm
ms.technology: vs-devops-reporting
ms.assetid: BF30FE4E-0370-4C9B-A660-51207D816F8B
ms.manager: greggboe
ms.author: jozimm
ms.date: 10/30/2017
---

# Performance and Latency
This document provides an overview of important considerations related to performance and data latency when using [Analytics](./what-is-analytics.md) for reporting.

## Performance
Analytics is designed to respond to any [aggregation](aggregated-data-analytics) following the [recommended query patterns](../extend-analytics/odata-query-guidelines.md) within ```3 to 5 seconds```.  

If a [non-aggregated query](../extend-analytics/analytics-recipes.md) exceeds 10,000 results the response will be paged. Depending on the complexity of filters($filter) or the number of selected Properties($select) the response time will vary between ```1 to 30 seconds```. Entities specifically designed for aggregations will be blocked as outlined in the [recommended query patterns](../extend-analytics/odata-query-guidelines.md) 

## Latency
Analytics is built on a curated copy of the data stored in Visual Studio Team Services (VSTS). Creating a copy of the data helps optimize read and aggregation performance and greatly reduces the impact reporting scenarios have on VSTS.

Copying the data also means that Analytics is ```not real-time```.  The process of copying the data introduces a ```5 to 30 second delay``` before the data associated with any change is represented in Analytics. 

### Data modeling
Publishing data models based on Analytics will introduce additional latency based on how frequently the model is refreshed.  Refreshing the model on a predefined interval is possible using tools such as [Power BI.com](../powerbi/overview.md).  At this time Analytics does not provide support for any real-time data modeling such as Power BI Direct Query.

### Installing Analytics
When installing the [Analytics Marketplace Extension](https://marketplace.visualstudio.com/items?itemName=ms.vss-analytics) the initial setup process usually takes between ```5 to 30 minutes```. If you are unable to access Analytics after a 24 hour period please contact [Microsoft Support](todo) 
