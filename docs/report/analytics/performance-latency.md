---
title: Performance and Latency of the Analytics Service for VSTS | VSTS  
description: S 
ms.prod: vs-devops-alm
ms.technology: vs-devops-reporting
ms.assetid: BF30FE4E-0370-4C9B-A660-51207D816F8B
ms.manager: greggboe
ms.author: jozimm
ms.date: 10/30/2017
---

# Performance and Latency of the Analytics Service for VSTS
When you use the Analytics Service for reporting, you’ll want to understand the performance and data latency issues associated with the service. To get started using the Analytics Service, see What is the[Analytics Service](./what-is-analytics.md).

## Installing Analytics
When you install the [Analytics Marketplace Extension](https://marketplace.visualstudio.com/items?itemName=ms.vss-analytics), you should expect the initial setup to take between ```5 to 30 minutes```. If after 24 hours you aren't able to access your data, contact [Microsoft Support](https://docs.microsoft.com/en-us/vsts/user-guide/provide-feedback?toc=/vsts/user-guide/toc.json&bc=/vsts/user-guide/breadcrumb/toc.json) 

## Performance
Using the [recommended query patterns](../extend-analytics/odata-query-guidelines.md), the Analytics Service will respond to any [aggregation](../extend-analytics/aggregated-data-analytics.md) or [non-aggregated query](../extend-analytics/analytics-recipes.md) query within 3 to 5 seconds. The query response will be paged if it exceeds 10,000 results. 

Any Entities specifically designed for aggregations that are used in a non-aggregated query will be blocked as outlined in the [recommended query patterns](../extend-analytics/odata-query-guidelines.md) 

## Latency
When you use Analytics, you query a curated copy of the data stored in Visual Studio Team Services (VSTS) for your account or a team project(s). The data copy helps optimize read and aggregation performance, and greatly reduces the impact reporting scenarios have on VSTS.

Because the data is copied, the Analytics service is ```not a real-time dta store```.  Copying the data introduces a ```5 to 30 second delay``` before the data associated with any one change shows up in Analytics. 

### Data modeling
Publishing a data model to [Power BI.com](../powerbi/overview.md) introduces additional data latency because OData is not supported by Power BI Direct Query.  The amount of additional latency is tied to how frequently the model is refreshed.  Power BI.com supports refreshing a data model manually or on a predefined interval.


