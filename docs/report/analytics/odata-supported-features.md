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

The following tables summarizes the supported and unsupported OData features.  

## Supported clauses

- ```$apply``` 
- ```$filter```
- ```$select``` 
- ```$top```  
- ```$skip```  
- ```$orderby```  
- ```$expand```  
- ```$count``` 

When multiple clauses are used in query they will be applied in the order specified above. Order of clauses in query string ignored. For example, in the following query, first work items are grouped and aggregated. Next, the groups are filtered. After that, the filtered groups are sorted. Finally, the first 5 records are returned. This means the query returns the top 5 work item types used at least 100 times.
``` 
WorkItems?$filter=Count ge 100$apply=groupby((WorkItemType), aggregate($count as Count))&&$orderby=Count&top=5
```
### Aggregation extensions support
$apply triggers aggregation behavior. It takes a sequence of set transformations, separated by forward slashes to express that they are consecutively applied, i.e. the result of each transformation is the input to the next transformation. For example in the following query, first work item are filtered. Next, grouped by work item type and state. Then groups are filtered and grouped again.

> [!NOTE]  
> OData aggregation extensions are relatively new and not yet fully supported by various client tools. 

``` 
Workitems?$apply=filter(State ne 'Closed')/groupby((WorkItemType, State), aggregate($count as Count))/filter(Count gt 100)/groupby((State),aggregate(Count with max as MaxCount))  
``` 

The following transformations are supported:
| Transformation | Notes |
| ------------------ | ----------- |
| ```groupby```  | Allows grouping by properties|
| ```filter```| Allows filtering input set. Supports the same expressions as ```$filter``` |  
| ```aggregate```  | Allows aggregation using one of following methods   ```$count```, ```average```, ```max```,  ```min```, ```sum```  |

For more details, see [Aggregate data](aggregated-data-analytics.md)

<a id="supported-functions"></a> 
## Supported functions
| Canonical function | Description |
| ------------------ | ----------- |  
| ```contains``` |  Returns true if the second parameter string value is a substring of the first parameter string value, otherwise it returns false  |  
| ```endswith``` | Returns true if the first parameter string value ends with the second parameter string value, otherwise it returns false |  
| ```startswith``` |  Returns true if the first parameter string value starts with the second parameter string value, otherwise it returns false |  
| ```length``` | Returns the number of characters in the parameter value |  
| ```indexof``` | Returns the zero-based character position of the first occurrence of the second parameter value in the first parameter value or -1 if the second parameter value does not occur in the first parameter value|  
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
| ``` maxdatetime``` | Returns the latest possible point in time as a DateTimeOffset value |  
| ```mindatetime``` |  Returns the earliest possible point in time as a DateTimeOffset value |  




OData functions are used in a ```$filter``` clause, but not in a ```$select``` clause the way they would be uses in a SQL statement.  

For example, you can specify:  

```
/WorkItems?$filter=toupper(Title) eq 'HELP' 
```
However, you can't enter the following: 
```
/WorkItems?$select=WorkItemId,State,toupper(Title)
```  

## Not supported features

- ```$search```  
- ```$compute```  
- ```$rollup```  
- ```$crossjoin```  
- ```concat```  
- ```compute```  
- ```isdefined```  
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