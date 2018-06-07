---
title: Enabling a Built-in Accessibility Feature
ms.assetid: f97a445d-f93d-4462-bce5-d853f5076b9c
description: 
ms.technology: desktop
ms.prod: windows
ms.author: windowssdkdev
ms.topic: article
ms.date: 05/31/2018
---

# Enabling a Built-in Accessibility Feature

The following code fragment uses the [**SystemParametersInfo**](https://msdn.microsoft.com/library/windows/desktop/ms724947) function to enable the FilterKeys feature:


```C++
FILTERKEYS fk; 
BOOL bSuccess; 
 
// Fill in the members of the FILTERKEYS structure.  
 
fk.cbSize = sizeof(FILTERKEYS); 
fk.dwFlags = (FKF_FILTERKEYSON | FKF_HOTKEYACTIVE | 
                       FKF_AVAILABLE | FKF_HOTKEYSOUND |
FKF_CLICKON); 
fk.iWaitMSec = 1000; 
fk.iDelayMSec = 1000; 
fk.iRepeatMSec = 500; 
fk.iBounceMSec = 0; 
 
// Call SystemParametersInfo with the SPI_SETFILTERKEYS flag.  
 
bSuccess = SystemParametersInfo(SPI_SETFILTERKEYS, 0, (LPVOID)
&amp;fk, 0); 
```



 

 



