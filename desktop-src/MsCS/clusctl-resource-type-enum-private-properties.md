---
title: CLUSCTL\_RESOURCE\_TYPE\_ENUM\_PRIVATE\_PROPERTIES control code
description: Retrieves a list of the read/write and read-only resource type private properties.
audience: developer
author: REDMOND\\markl
manager: REDMOND\\markl
ms.assetid: '44b4752f-69aa-4082-9912-02ffa7a18d0c'
ms.prod: 'windows-server-dev'
ms.technology: 'failover-clustering'
ms.tgt_platform: multiple
keywords: ["CLUSCTL_RESOURCE_TYPE_ENUM_PRIVATE_PROPERTIES control code Failover Cluster"]
topic_type:
- apiref
api_name:
- CLUSCTL_RESOURCE_TYPE_ENUM_PRIVATE_PROPERTIES
api_location:
- ClusAPI.h
api_type:
- HeaderDef
---

# CLUSCTL\_RESOURCE\_TYPE\_ENUM\_PRIVATE\_PROPERTIES control code

Retrieves a list of the read/write and read-only [resource type](resource-types.md) [private properties](private-properties.md). Applications use this [control code](about-control-codes.md) as a [**ClusterResourceTypeControl**](clusterresourcetypecontrol.md) parameter, and [resource DLLs](resource-dlls.md) receive the control code as a [**ResourceTypeControl**](resourcetypecontrol.md) parameter.


```C++
ClusterResourceTypeControl( 
  hCluster,                                          // cluster handle
  lpszResTypeName,                                   // resource type name
  hHostNode,                                         // optional host node
  CLUSCTL_RESOURCE_TYPE_ENUM_PRIVATE_PROPERTIES,     // this control code
  NULL,                                              // input buffer (not used)
  0,                                                 // input buffer size (not used)
  lpOutBuffer,                                       // output buffer: array of strings
  cbOutBufferSize,                                   // allocated buffer size (bytes)
  lpcbBytesReturned );                               // actual size of resulting data (bytes)
```



## Parameters

The following control code function and DLL support parameter is specific to this control code. For complete parameter descriptions, see [**ClusterResourceTypeControl**](clusterresourcetypecontrol.md) or [**ResourceTypeControl**](resourcetypecontrol.md).

<dl> <dt>

*lpOutBuffer* 
</dt> <dd>

On a successful return, contains an array of null-terminated Unicode strings with an additional **NULL** terminator appended to the last string. Each string in the array contains the name of a read/write private resource type property.

</dd> </dl>

## Return value

[**ClusterResourceTypeControl**](clusterresourcetypecontrol.md) returns one of the following values.

<dl> <dt>

**ERROR\_SUCCESS**
</dt> <dd>

0

The operation completed successfully.

</dd> <dt>

**ERROR\_MORE\_DATA**
</dt> <dd>

234 (0xEA)

More data is available. The output buffer pointed to by *lpOutBuffer* was not large enough to hold the data resulting from the operation. The *lpcbBytesReturned* parameter points to the size required for the output buffer.

</dd> <dt>

**[System error code](https://msdn.microsoft.com/library/windows/desktop/ms681381)**
</dt> <dd>

If any other value is returned, then the operation failed. The value of *lpcbBytesReturned* is unreliable.

</dd> </dl>

## Remarks

The CLUSCTL\_RESOURCE\_TYPE\_ENUM\_PRIVATE\_PROPERTIES control code returns only property names, not property values. To retrieve values for common resource type properties, use [CLUSCTL\_RESOURCE\_TYPE\_GET\_PRIVATE\_PROPERTIES](clusctl-resource-type-get-private-properties.md) and [CLUSCTL\_RESOURCE\_TYPE\_GET\_RO\_PRIVATE\_PROPERTIES](clusctl-resource-type-get-ro-private-properties.md).

For more information, see [Getting Information with Control Codes](getting-information-with-control-codes.md).

ClusAPI.h defines the 32 bits of CLUSCTL\_RESOURCE\_TYPE\_ENUM\_PRIVATE\_PROPERTIES as follows (for more information, see [Control Code Architecture](control-code-architecture.md)).



| Component      | Bit location | Value                                       |
|----------------|--------------|---------------------------------------------|
| Object code    | 24�31        | **CLUS\_OBJECT\_RESOURCE\_TYPE** (0x2)      |
| Global bit     | 23           | **CLUS\_NOT\_GLOBAL** (0x0)                 |
| Modify bit     | 22           | **CLUS\_NO\_MODIFY** (0x0)                  |
| User bit       | 21           | **CLCTL\_CLUSTER\_BASE** (0x0)              |
| Type bit       | 20           | External (0x0)                              |
| Operation code | 0�23         | **CLCTL\_ENUM\_PRIVATE\_PROPERTIES** (0x79) |
| Access code    | 0�1          | **CLUS\_ACCESS\_READ** (0x1)                |



�

### Resource DLL Support

Required. Always support the CLUSCTL\_RESOURCE\_TYPE\_ENUM\_PRIVATE\_PROPERTIES control code by returning the names of the resource type's private properties in the *OutBuffer* parameter.

As a general guideline, the Resource Monitor should handle all of the control codes for [common properties](common-properties.md), while your DLL should handle all control codes for [private properties](private-properties.md).

For more information on the [**ResourceTypeControl**](resourcetypecontrol.md) entry point, see [Implementing ResourceTypeControl](implementing-resourcetypecontrol.md).

## Requirements



|                                     |                                                                                      |
|-------------------------------------|--------------------------------------------------------------------------------------|
| Minimum supported client<br/> | None supported<br/>                                                            |
| Minimum supported server<br/> | Windows Server�2008 Enterprise, Windows Server�2008 Datacenter<br/>            |
| Header<br/>                   | <dl> <dt>ClusAPI.h</dt> </dl> |



## See also

<dl> <dt>

[External Resource Type Control Codes](external-resource-type-control-codes.md)
</dt> <dt>

[CLUSCTL\_RESOURCE\_TYPE\_GET\_COMMON\_PROPERTIES](clusctl-resource-type-get-common-properties.md)
</dt> <dt>

[CLUSCTL\_RESOURCE\_TYPE\_GET\_RO\_COMMON\_PROPERTIES](clusctl-resource-type-get-ro-common-properties.md)
</dt> <dt>

[**ClusterResourceTypeControl**](clusterresourcetypecontrol.md)
</dt> <dt>

[**ResourceTypeControl**](resourcetypecontrol.md)
</dt> </dl>

�

�




