---
title: Supported OData features   
description: Current level of support for OData specification in the Analytics Service
ms.prod: vs-devops-alm
ms.technology: vs-devops-reporting
ms.assetid: 8D81FEFD-F432-4E10-A415-9167B5FE9A57 
ms.manager: douge
ms.author: kokosins
ms.date: 11/15/2017
---


# Supported OData features  

The following table summarizes the supported and unsupported OData functions.  

> [!NOTE]  
> OData aggregation extensions are relatively new and either not supported by various client tools (yet) or full support for the extension is not supported by the Analytics Service.  

## Supported clauses

- ```$apply``` 
- ```$filter```
- ```$select``` 
- ```$top```  
- ```$skip```  
- ```$orderby```  
- ```$expand```  
- ```$count``` 

When multiple clauses are used in query they will be applied to order as specified above. For example, in following query, first we will group by and aggregate, then filter, then sort and take first 5 records to get top 5 work item types used at least 100 times:
``` 
WorkItems?$apply=groupby((WorkItemType), aggregate($count as Count))&$filter=Count ge 100&$orderby=Count&top=5
```

$apply clause allow to transform input. Multiple transformations could be combined with ```/```. For example:
``` 
Workitems?$apply=filter(State ne 'Closed')/groupby((WorkItemType), aggregate($count as Count))  
``` 

Following transformations are supported:
| Transformation | Notes |
| ------------------ | ----------- |
| ```groupby```  | Allows to group by properties|
| ```filter```| Allows to filter input. Supports the same expressions as ```$filter``` |  
| ```aggregate```  | Allows to aggregate using one of following methods   ```$count```, ```average```, ```max```,  ```min```, ```sum```  |

For more samples, see [Aggregate data](aggregated-data-analytics.md)

<a id="supported-functions"></a> 
## Supported functions
| Canonical function | Description |
| ------------------ | ----------- |  
| ```contains``` |  Returns true if the second parameter string value is a substring of the first parameter string value, otherwise it returns false.  |  
| ```endswith``` | Returns true if the first parameter string value ends with the second parameter string value, otherwise it returns false |  
| ```startswith``` |  Returns true if the first parameter string value starts with the second parameter string value, otherwise it returns false |  
| ```length``` | Returns the number of characters in the parameter value |  
| ```indexof``` | Returns the zero-based character position of the first occurrence of the second parameter value in the first parameter value |  
| ```substring``` | Returns a substring of the first parameter string value, starting at the Nth character and finishing at the last character (where N is the second parameter integer value) |  
| ```tolower``` |  Returns the input parameter string value with all uppercase characters converted to lowercase  |  
| ```toupper``` |  Returns  the input parameter string value with all lowercase characters converted to uppercase |  
| ```trim``` |  Returns the input parameter string value with all leading and trailing whitespace characters |  
| ```concat``` | Returns the year component of the Date or DateTimeOffset parameter value |  
| ```year``` |  Returns the year component of the Date or DateTimeOffset parameter value |  
| ```month``` | Returns the month component of the Date or DateTimeOffset parameter value |  
| ```day``` |  Returns the day component of the Date or DateTimeOffset parameter value |  
| ```second``` | Returns the second component (without the fractional part) of the DateTimeOffset or TimeOfDay parameter value |  
| ```fractionalseconds``` |  Returns the fractional seconds component of the DateTimeOffset or TimeOfDay parameter value as a non-negative decimal value less than 1 |  
| ```date``` | Returns the date part of the DateTimeOffset parameter value |  
| ```time``` |  Returns the time part of the DateTimeOffset parameter value |  
| ```totaloffsetminutes``` | Returns  the signed number of minutes in the time zone offset part of the DateTimeOffset parameter value |  
| ```now``` |  Returns the current point in time (date and time with time zone) as a DateTimeOffset value |  
| ``` maxdatetime``` | Returns  the latest possible point in time as a DateTimeOffset value |  
| ```mindatetime``` |  Returns the earliest possible point in time as a DateTimeOffset value |  




You use OData functions in a ```filter``` clause, but not in a ```$select``` clause the way that you would use them in a SQL statement.  

For example, you can specify:  

```
/WorkItems?$filter=toupper(Title) eq 'HELP' 
```
However, you can't enter the following: 
```
/WorkItems?$select=WorkItemId,State,toupper(Title)
```  

## Not supported clauses, expressions or transformations

- ```concat```  
- ```$search```  
- ```$compute```  
- ```compute```  
- ```$rollup```  
- ```isdefined```  
- ```$crossjoin```  
- ```topcount```  
- ```topsum```  
- ```toppercent```  
- ```bottomcount```  
- ```bottomsum```  
- ```bottompercent```  
- ```countdistinct```  
- ```from``` 

## Related notes  

- [WIT analytics](wit-analytics.md)  
- [Aggregate data](aggregated-data-analytics.md)
- [OData v4.0 specification](http://www.odata.org/documentation/)  
- [OData v4.0 Part 2: URL Conventions Plus Errata 02](http://docs.oasis-open.org/odata/odata/v4.0/errata02/os/complete/part2-url-conventions/odata-v4.0-errata02-os-part2-url-conventions-complete.html)
- [OData v4.0 Aggregation Extension](http://docs.oasis-open.org/odata/odata-data-aggregation-ext/v4.0/odata-data-aggregation-ext-v4.0.html)