---
title: Setting Permissions to a Specific Property
description: Permissions can be set to apply to a specific property of an object.
audience: developer
author: REDMOND\\markl
manager: REDMOND\\mbaldwin
ms.assetid: 7bafba5a-a437-4777-98a0-f478b738a8ca
ms.prod: windows-server-dev
ms.technology: active-directory-domain-services
ms.tgt_platform: multiple
keywords:
- Setting Permissions to a Specific Property AD
ms.author: windowssdkdev
ms.topic: article
ms.date: 05/31/2018
---

# Setting Permissions to a Specific Property

Permissions can be set to apply to a specific property of an object.

**To set permissions that apply to a specific property of an object**

1.  Set the [**IADsAccessControlEntry.AccessMask**](https://msdn.microsoft.com/library/aa705952) property to **ADS\_RIGHT\_DS\_READ\_PROP** and/or **ADS\_RIGHT\_DS\_WRITE\_PROP**.
2.  Set the [**IADsAccessControlEntry.AceType**](https://msdn.microsoft.com/library/aa705952) property to **ADS\_ACETYPE\_ACCESS\_ALLOWED\_OBJECT** or **ADS\_ACETYPE\_ACCESS\_DENIED\_OBJECT**.
3.  Set the [**IADsAccessControlEntry.ObjectType**](https://msdn.microsoft.com/library/aa705952) property to the **schemaIDGUID** of the property. This is the **schemaIDGUID** of the **attributeSchema** object that defines the property in the schema. The GUID must be specified as a string of the form produced by the [**StringFromGUID2**](5f437658-b749-416b-805a-2afdac682660) function in the COM library.
4.  Set [**IADsAccessControlEntry.Flags**](https://msdn.microsoft.com/library/aa705952) to **ADS\_FLAG\_OBJECT\_TYPE\_PRESENT**.

For more information about the **schemaIDGUID** of a predefined attribute, see [Active Directory Domain Services Reference](active-directory-domain-services-reference.md).

For more information and a code example that can be used to retrieve a schemaIDGUID, see [Reading attributeSchema and classSchema Objects](reading-attributeschema-and-classschema-objects.md).

For more information about how to create an ACE, see [Setting Access Rights on an Object](setting-access-rights-on-an-object.md).

For more information and a code example that can be used to set a property-specific ACE, see [Example Code for Setting an ACE on a Directory Object](example-code-for-setting-an-ace-on-a-directory-object.md).

 

 



