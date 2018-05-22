---
title: EM\_SETIMESTATUS message
description: Sets the status flags that determine how an edit control interacts with the Input Method Editor (IME).
ms.assetid: '3de2e8b5-bdd8-4b25-9427-38a11b77a17a'
keywords: ["EM_SETIMESTATUS message Windows Controls"]
topic_type:
- apiref
api_name:
- EM_SETIMESTATUS
api_location:
- Winuser.h
api_type:
- HeaderDef
---

# EM\_SETIMESTATUS message

Sets the status flags that determine how an edit control interacts with the Input Method Editor (IME).

## Parameters

<dl> <dt>

*wParam* 
</dt> <dd>

The type of status to set. This parameter can be the following value.



| Value                                                                                                                                                                                       | Meaning                                                       |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------|
| <span id="EMSIS_COMPOSITIONSTRING"></span><span id="emsis_compositionstring"></span><dl> <dt>**EMSIS\_COMPOSITIONSTRING**</dt> </dl> | Sets behavior for the handling composition string.<br/> |



�

</dd> <dt>

*lParam* 
</dt> <dd>

Data specific to the status type. If *wParam* is **EMSIS\_COMPOSITIONSTRING**, this parameter can be one or more of the following values.



| Value                                                                                                                                                                                                            | Meaning                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span id="EIMES_GETCOMPSTRATONCE"></span><span id="eimes_getcompstratonce"></span><dl> <dt>**EIMES\_GETCOMPSTRATONCE**</dt> </dl>                         | If this flag is set, the edit control hooks the [**WM\_IME\_COMPOSITION**](https://msdn.microsoft.com/library/windows/desktop/dd374133) message with *lParam* set to GCS\_RESULTSTR and returns the result string immediately. If this flag is not set, the edit control passes the **WM\_IME\_COMPOSITION** message to the default window procedure and handles the result string from the [**WM\_CHAR**](https://msdn.microsoft.com/library/windows/desktop/ms646276) message; this is the default behavior of the edit control.<br/> |
| <span id="EIMES_CANCELCOMPSTRINFOCUS"></span><span id="eimes_cancelcompstrinfocus"></span><dl> <dt>**EIMES\_CANCELCOMPSTRINFOCUS**</dt> </dl>             | If this flag is set, the edit control cancels the composition string when it receives the [**WM\_SETFOCUS**](https://msdn.microsoft.com/library/windows/desktop/ms646283) message. If this flag is not set, the edit control does not cancel the composition string; this is the default behavior of the edit control.<br/>                                                                                                                                                                     |
| <span id="EIMES_COMPLETECOMPSTRKILLFOCUS"></span><span id="eimes_completecompstrkillfocus"></span><dl> <dt>**EIMES\_COMPLETECOMPSTRKILLFOCUS**</dt> </dl> | If this flag is set, the edit control completes the composition string upon receiving the [**WM\_KILLFOCUS**](https://msdn.microsoft.com/library/windows/desktop/ms646282) message. If this flag is not set, the edit control does not complete the composition string; this is the default behavior of the edit control.<br/>                                                                                                                                                                 |



�

</dd> </dl>

## Return value

Returns the previous value of the *lParam* parameter.

## Remarks

**Rich Edit:** The **EM\_SETIMESTATUS** message is not supported.

## Requirements



|                                     |                                                                                                          |
|-------------------------------------|----------------------------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows�Vista \[desktop apps only\]<br/>                                                           |
| Minimum supported server<br/> | Windows Server�2003 \[desktop apps only\]<br/>                                                     |
| Header<br/>                   | <dl> <dt>Winuser.h (include Windows.h)</dt> </dl> |



## See also

<dl> <dt>

[**EM\_GETIMESTATUS**](em-getimestatus.md)
</dt> </dl>

�

�




