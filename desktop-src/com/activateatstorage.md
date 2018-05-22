---
title: ActivateAtStorage
description: Configures the client to instantiate objects on the same computer as the persistent state they are using or from which they are initialized.
ms.assetid: 'bc0f0c1c-dbfc-4b7a-b897-3646afe3f6bb'
keywords: ["registry value COM"]
---

# ActivateAtStorage

Configures the client to instantiate objects on the same computer as the persistent state they are using or from which they are initialized.

## Registry Entry

```
HKEY_LOCAL_MACHINE\SOFTWARE\Classes\AppID
   {AppID_GUID}
      ActivateAtStorage = value
```

## Remarks

This is a **REG\_SZ** value. Any value that begins with 'Y' or 'y' indicates that **ActivateAtStorage** should be used.

The **ActivateAtStorage** capability provides a transparent way to allow clients to locate running objects on the same computer as the data that they use. This reduces network traffic because the object performs local file-system calls instead of calls across the network.

When a value is set for **ActivateAtStorage**, this becomes the default behavior in calls to the [**CoGetInstanceFromFile**](cogetinstancefromfile.md) and [**CoGetInstanceFromIStorage**](cogetinstancefromistorage.md) functions, as well as to the file moniker implementation of [**IMoniker::BindToObject**](imoniker-bindtoobject.md). In all of these calls, specifying a [**COSERVERINFO**](coserverinfo.md) structure overrides the setting of **ActivateAtStorage** for the duration of the function call. The caller can pass **COSERVERINFO** information to **IMoniker::BindToObject** through the [**BIND\_OPTS2**](bind-opts2.md) structure.

The value set for **ActivateAtStorage** is also the default behavior when CLSCTX\_REMOTE\_SERVER is specified if no registry information for the class is installed on the client's computer. Client applications written to take advantage of **ActivateAtStorage** may therefore require less administration.

## Related topics

<dl> <dt>

[**CLSCTX**](clsctx.md)
</dt> <dt>

[**CoGetInstanceFromFile**](cogetinstancefromfile.md)
</dt> <dt>

[**CoGetInstanceFromIStorage**](cogetinstancefromistorage.md)
</dt> <dt>

[**COSERVERINFO**](coserverinfo.md)
</dt> <dt>

[**IMoniker::BindToObject**](imoniker-bindtoobject.md)
</dt> <dt>

[Registering COM Servers](registering-com-servers.md)
</dt> </dl>

 

 



