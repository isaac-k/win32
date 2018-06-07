---
title: Remote Desktop Services API Structures
description: Lists structures that are used with the Remote Desktop Services API.
audience: developer
author: REDMOND\\markl
manager: REDMOND\\markl
ms.assetid: 5d467241-499c-4038-8d9c-4244457e484f
ms.prod: windows-server-dev
ms.technology: remote-desktop-services
ms.tgt_platform: multiple
ms.author: windowssdkdev
ms.topic: article
ms.date: 05/31/2018
---

# Remote Desktop Services API Structures

The following structures are used with the Remote Desktop Services API.

## In this section

<dl> <dt>

[**CHANNEL\_DEF**](/windows/desktop/api/Pchannel/ns-pchannel-tagchannel_def)
</dt> <dd>

Contains the name and options of a Remote Desktop Services virtual channel.

</dd> <dt>

[**CHANNEL\_ENTRY\_POINTS**](/windows/desktop/api/Cchannel/ns-cchannel-tagchannel_entry_points)
</dt> <dd>

Contains pointers to the functions called by a client-side DLL to access virtual channels.

</dd> <dt>

[**CHANNEL\_PDU\_HEADER**](/windows/desktop/api/Pchannel/ns-pchannel-tagchannel_pdu_header)
</dt> <dd>

Contains information about a data block being received by the server end of a virtual channel.

</dd> <dt>

[**LSKeyPack**](lskeypack.md)
</dt> <dd>

Contains information about a specific Remote Desktop Services licensing key pack.

</dd> <dt>

[**LSLicense**](lslicense.md)
</dt> <dd>

Contains information about a specific Remote Desktop Services license.

</dd> <dt>

[**WTSCLIENT**](/windows/desktop/api/Wtsapi32/ns-wtsapi32-_wtsclienta)
</dt> <dd>

Contains information about a Remote Desktop Connection (RDC) client.

</dd> <dt>

[**WTSCONFIGINFO**](/windows/desktop/api/Wtsapi32/ns-wtsapi32-_wtsconfiginfoa)
</dt> <dd>

Contains information about a Remote Desktop Services session.

</dd> <dt>

[**WTSINFO**](/windows/desktop/api/Wtsapi32/ns-wtsapi32-_wtsinfoa)
</dt> <dd>

Contains information about a Remote Desktop Services session.

</dd> <dt>

[**WTSINFOEX**](/windows/desktop/api/Wtsapi32/ns-wtsapi32-_wtsinfoexa)
</dt> <dd>

Contains a [**WTSINFOEX\_LEVEL**](/windows/desktop/api/Wtsapi32/ns-wtsapi32-_wtsinfoex_level_a) union that contains extended information about a Remote Desktop Services session.

</dd> <dt>

[**WTSINFOEX\_LEVEL1**](/windows/desktop/api/Wtsapi32/ns-wtsapi32-_wtsinfoex_level1_a)
</dt> <dd>

Contains extended information about a Remote Desktop Services session.

</dd> <dt>

[**WTSLISTENERCONFIG**](/windows/desktop/api/Wtsapi32/ns-wtsapi32-_wtslistenerconfiga)
</dt> <dd>

Contains information about a Remote Desktop Services listener.

</dd> <dt>

[**WTSSBX\_IP\_ADDRESS**](/windows/desktop/api/Tssbx/ns-tssbx-__midl_iwtssbplugin_0004)
</dt> <dd>

Contains information about the IP address of a network resource.

</dd> <dt>

[**WTSSBX\_MACHINE\_CONNECT\_INFO**](/windows/desktop/api/Tssbx/ns-tssbx-__midl_iwtssbplugin_0006)
</dt> <dd>

Contains information about a computer that is accepting remote connections.

</dd> <dt>

[**WTSSBX\_MACHINE\_INFO**](/windows/desktop/api/Tssbx/ns-tssbx-__midl_iwtssbplugin_0007)
</dt> <dd>

Contains information about a computer and its current state.

</dd> <dt>

[**WTSSBX\_SESSION\_INFO**](/windows/desktop/api/Tssbx/ns-tssbx-__midl_iwtssbplugin_0009)
</dt> <dd>

Contains information about sessions that are available to Remote Desktop Connection Broker (RD Connection Broker).

</dd> <dt>

[**WTSSESSION\_NOTIFICATION**](/windows/desktop/api/Winuser/ns-winuser-tagwtssession_notification)
</dt> <dd>

Provides information about the session change notification. A service receives this structure in its [*HandlerEx*](https://msdn.microsoft.com/library/windows/desktop/ms683241) function in response to a session change event.

</dd> <dt>

[**WTSUSERCONFIG**](/windows/desktop/api/Wtsapi32/ns-wtsapi32-_wtsuserconfiga)
</dt> <dd>

Contains configuration information for a user on a domain controller or Remote Desktop Session Host (RD Session Host) server.

</dd> <dt>

[**WTS\_CLIENT\_ADDRESS**](/windows/desktop/api/Wtsapi32/ns-wtsapi32-_wts_client_address)
</dt> <dd>

Contains the client network address of a Remote Desktop Services session.

</dd> <dt>

[**WTS\_CLIENT\_DISPLAY**](/windows/desktop/api/Wtsapi32/ns-wtsapi32-_wts_client_display)
</dt> <dd>

Contains information about the display of a Remote Desktop Connection (RDC) client.

</dd> <dt>

[**WTS\_PROCESS\_INFO**](/windows/desktop/api/Wtsapi32/ns-wtsapi32-_wts_process_infoa)
</dt> <dd>

Contains information about a process running on a RD Session Host server.

</dd> <dt>

[**WTS\_PROCESS\_INFO\_EX**](/windows/desktop/api/Wtsapi32/ns-wtsapi32-_wts_process_info_exa)
</dt> <dd>

Contains extended information about a process running on a RD Session Host server.

</dd> <dt>

[**WTS\_PRODUCT\_INFO**](/windows/desktop/api/Wtsapi32/)
</dt> <dd>

The details of the product license that is required to connect to a terminal server.

</dd> <dt>

[**WTS\_SERVER\_INFO**](/windows/desktop/api/Wtsapi32/ns-wtsapi32-_wts_server_infoa)
</dt> <dd>

Contains information about a specific Remote Desktop Services server.

</dd> <dt>

[**WTS\_SESSION\_ADDRESS**](/windows/desktop/api/Wtsapi32/ns-wtsapi32-_wts_session_address)
</dt> <dd>

Contains the virtual IP address assigned to a session.

</dd> <dt>

[**WTS\_SESSION\_INFO**](/windows/desktop/api/Wtsapi32/ns-wtsapi32-_wts_session_infoa)
</dt> <dd>

Contains information about a client session on a RD Session Host server.

</dd> <dt>

[**WTS\_SESSION\_INFO\_1**](/windows/desktop/api/Wtsapi32/ns-wtsapi32-_wts_session_info_1a)
</dt> <dd>

Contains extended information about a client session on a RD Session Host server or Remote Desktop Virtualization Host (RD Virtualization Host) server.

</dd> </dl>

 

 



