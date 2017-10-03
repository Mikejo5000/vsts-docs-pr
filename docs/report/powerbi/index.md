---
title: VSTS & Power BI | VSTS 
description: Index to topics for generating PowerBI charts, reports, and dashboards for VSTS and and Team Foundation Server (TFS)  
ms.assetid:  
ms.prod: vs-devops-alm
ms.technology: vs-devops-reporting
ms.manager: douge
ms.author: kaelli
ms.date: 08/03/2017
---

# VSTS & PowerBI 


<b>VSTS</b> 

>[!NOTE]  
> **Feature availability:**  Using the Power BI Content Pack, you can generate PowerBI dashboards and reports. The Power BI Data Connector, however, requires access to the Analytics Service. The Analytics Service is in a closed preview at this time.  
>  
> Both the Power BI Content Pack and Power BI Data Connector are only available for VSTS.  

<!---

## Overview  
[Power BI integration overview](overview.md)
-->


## How-to Guides

- [Assign Analytics permissions (Security)](../analytics/analytics-security.md?toc=/vsts/report/powerbi/toc.json&bc=/vsts/report/powerbi/breadcrumb/toc.json)  

### Power BI Data Connector
The Data Connector allows users to select the data they are interested in, and includes support for a fully customized data model by including project-specific fields, work item customizations, and adding tables from additional data sources. Users can consume default views from VSTS, or generate custom views for use in PowerBI.
- [Connect to Power BI via the Data Connector](data-connector-connect.md)     
- [Power BI desktop and OData aggregations](../analytics/using-odata-aggregations-with-power-bi-desktop.md?toc=/vsts/report/powerbi/toc.json&bc=/vsts/report/powerbi/breadcrumb/toc.json)    
- [Share reports, publish to PowerBI.com](../analytics/publishing-power-bi-desktop-to-power-bi.md?toc=/vsts/report/powerbi/toc.json&bc=/vsts/report/powerbi/breadcrumb/toc.json)    

### Power BI Content Pack 
The Content Pack, contains a complete analytic data model (tables, relationships and measures), a set of default reports and a default dashboard. Reports and dashboard are fully customizable but the data model is not. All VSTS customers can use the Content Pack to generate dashboards and reports.
- [Connect to VSTS with Power BI Content Pack](connect-vso-pbi-vs.md)  
- [Create dashboards and reports](report-on-vso-with-power-bi-vs.md) 
- [Create trend charts](create-trend-charts.md)  
- [Create rollup charts](create-rollup-charts.md) 
  
## Reference
- [Analytics Schema Model] (..\todo.md)
- [Analytics Metadata API] (..\todo.md)
- [Analytics Query Limits & Tuning] (..\todo.md)
### Power BI Data Connector
- [Data Connector functions and limitations](data-connector-functions.md)- 
### Power BI Content Pack 
- [Data for Power BI Content pack](vso-pbi-whats-available-vs.md)    
- [Analytics Service overview](../analytics/overview-analytics-service.md?toc=/vsts/report/powerbi/toc.json&bc=/vsts/report/powerbi/breadcrumb/toc.json)    


## Resources 
- [Analytics OData Api](../todo.md)
- [Dashboards, charts, & widgets](../index.md)  
- [PowerBI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
- [PowerBI Documentation](https://powerbi.microsoft.com/documentation/powerbi-landing-page/)  
- [Insights Lab Power BI Widget](https://marketplace.visualstudio.com/items?itemName=InsightsLab.powerbiWidget) 
 

 
