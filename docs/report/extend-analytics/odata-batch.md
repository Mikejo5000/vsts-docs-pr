---
title: OData Batch Support | VSTS
description: Guidelines for extension developers who want to learn how to write good OData queries.
ms.prod: vs-devops-alm
ms.technology: vs-devops-reporting
ms.assetid: 
ms.manager: trevorc
ms.author: prprice
ms.date: 11/7/2017
---

# OData batch support
Batch requests are part of the OData spec, and the Analytics service provides limited support for them. For more information about batch operations in OData see section [11.7 Batch Requests](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part1-protocol/odata-v4.0-errata03-os-part1-protocol-complete.html#_Toc453752313) of the OData spec.


## The Analytics $batch endpoint
The $batch endpoint is located at ```https://{account}.analytics.visualstudio.com/_odata/{version}/$batch```. Note that the $batch endpoint is not available with a project scope, but the queries within a batch can contain project scoping.

### Supported $batch operations
The OData spec allows for numerous operations per $batch request, however the Analytics service limits each $batch request to a single query. The Analytics $batch endpoint is also read-only, no change sets may be published to it.

### When to use $batch queries
Many modern browsers have limits on the length of a request's URL. Exceeding this limit can result in undesired behavior. Using a $batch request allows long queries to be issued against the Analtyics service since the OData query is delivered in a POST body. You may use $batch requests for all your queries, though GET requests are slightly faster.

## $batch request examples

### $batch request with a single query
#### Request
URL: ```https://{account}.analytics.visualstudio.com/_odata/{version}/$batch```  
Content-Type: ```multipart/mixed; boundary=batch_2af9a11e-9dec-4266-a3ab-0db9d10fb55a```  
Request payload:
```
--batch_1af9a11e-9dec-4266-a3ab-0db9d10fb55a
Content-Type: application/http
Content-Transfer-Encoding: binary

GET https://{account}.analytics.vsts.me/_odata/{version}/Users?$filter=UserEmail eq 'john.smith@contosso.com'&$select=UserId,UserSK,UserName HTTP/1.1
Accept: application/json

--batch_1af9a11e-9dec-4266-a3ab-0db9d10fb55a
```
#### Response
Status code: ```200```  
Response body:  
```
--batchresponse_0cc7749e-dcec-4b5e-9380-eb05859fe733
Content-Type: application/http
Content-Transfer-Encoding: binary

HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
OData-Version: 4.0

{"@odata.context":"https://{account}.analytics.vsts.me/_odata/{version}/$metadata#Users(UserId,UserSK,UserName)","value":[{"UserId":"04713655-3724-6024-b9a4-f0b1c6202dbc","UserSK":"04713655-3724-6024-b9a4-f0b1c6202dbc","UserName":"John Smith"}]}
--batchresponse_0cc7749e-dcec-4b5e-9380-eb05859fe733--
```
### $batch request with multiple queries
#### Request
URL: ```https://{account}.analytics.visualstudio.com/_odata/{version}/$batch```  
Content-Type: ```multipart/mixed; boundary=batch_a21dac40-0b65-4e56-8101-73c79d508b39```  
Request payload:
```
--batch_1af9a11e-9dec-4266-a3ab-0db9d10fb55a
Content-Type: application/http
Content-Transfer-Encoding: binary

GET https://{account}.analytics.vsts.me/_odata/{version}/Users?$filter=UserEmail eq 'john.smith@contosso.com'&$select=UserId,UserSK,UserName HTTP/1.1
Accept: application/json

--batch_1af9a11e-9dec-4266-a3ab-0db9d10fb55a
Content-Type: application/http
Content-Transfer-Encoding: binary

GET https://{account}.analytics.vsts.me/_odata/{version}/Users?$filter=UserEmail eq 'john.smith@contosso.com'&$select=UserId,UserSK,UserName HTTP/1.1
Accept: application/json

--batch_1af9a11e-9dec-4266-a3ab-0db9d10fb55a
```
#### Response
Status Code: ```400```  
Response payload:
```
{
    "$id": "1",
    "innerException": null,
    "message": "The Analytics Service doesn’t support processing of multiple operations which the current batch message contains. The Analytics Service uses OData batch in order to support POST requests, but requires you limit the operation to a single request.",
    "typeName": "Microsoft.OData.ODataException, Microsoft.TeamFoundation.OData.Core",
    "typeKey": "ODataException",
    "errorCode": 0,
    "eventId": 0
}
```