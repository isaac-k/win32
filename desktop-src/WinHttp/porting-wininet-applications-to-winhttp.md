---
Description: 'Microsoft Windows HTTP Services (WinHTTP) is targeted at middle-tier and back-end server applications that require access to an HTTP client stack.'
ms.assetid: '5b0cf321-8f69-4526-a628-e6ca0f9d4a58'
title: Porting WinINet Applications to WinHTTP
---

# Porting WinINet Applications to WinHTTP

Microsoft Windows HTTP Services (WinHTTP) is targeted at middle-tier and back-end server applications that require access to an HTTP client stack. [Microsoft Windows Internet (WinINet)](winhttp-start-page.md) provides an HTTP client stack for client applications, as well as access to the File Transfer Protocol (FTP), SOCKSv4, and Gopher protocols. This overview can help determine whether porting your WinINet applications to WinHTTP would be beneficial. It also describes specific conversion requirements.

-   [Things to Consider Before Porting Your WinINet Application](#things-to-consider-before-porting-your-wininet-application)
-   [WinHTTP Equivalents to WinINet Functions](#winhttp-equivalents-to-wininet-functions)
-   [Different Handling of Asynchronous Requests](#different-handling-of-asynchronous-requests)
-   [Differences in WinHTTP Callback Notifications](#differences-in-winhttp-callback-notifications)
-   [Authentication Differences](#authentication-differences)
-   [Differences in Secure HTTP Transactions](#differences-in-secure-http-transactions)

## Things to Consider Before Porting Your WinINet Application

Consider porting your WinINet application to WinHTTP if your application would benefit from:

-   A server-safe HTTP client stack.
-   Minimized stack usage.
-   The scalability of a server application.
-   Fewer dependencies on platform-related APIs.
-   Support for thread impersonation.
-   A service-friendly HTTP stack.
-   Access to the scriptable [**WinHttpRequest**](winhttprequest.md) object.

Do not consider porting your WinINet application to WinHTTP if it must support one or more of the following:

-   The FTP or Gopher protocol from the HTTP stack.
-   Support for SOCKSv4 protocol for communicating with SOCKS proxies.
-   Automatic dial-up services.

If you decide to port your application to WinHTTP, the following sections guide you through the conversion process.

For a sample application for both WinINet and WinHTTP, compare the AsyncDemo sample for WinINet with the AsyncDemo sample for WinHTTP.

## WinHTTP Equivalents to WinINet Functions

The following table lists WinINet functions related to the HTTP client stack together with the WinHTTP equivalents.

If your application requires WinINet functions that are not listed, do not port your application to WinHTTP.



| WinINet function                                                       | WinHTTP equivalent                                                                                                                                                                                     | Notable changes                                                                                                                                                                                                                                                                                                                      |
|------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**HttpAddRequestHeaders**](https://msdn.microsoft.com/library/windows/desktop/aa384227)             | [**WinHttpAddRequestHeaders**](winhttpaddrequestheaders.md)                                                                                                                                           | None.                                                                                                                                                                                                                                                                                                                                |
| [**HttpEndRequest**](https://msdn.microsoft.com/library/windows/desktop/aa384230)                           | [**WinHttpReceiveResponse**](winhttpreceiveresponse.md)                                                                                                                                               | The context value is set with [**WinHttpSendRequest**](winhttpsendrequest.md) or [**WinHttpSetOption**](winhttpsetoption.md). Request options are set with [**WinHttpOpenRequest**](winhttpopenrequest.md). [**WinHttpReceiveResponse**](winhttpreceiveresponse.md) must be called after sending a request.                      |
| [**HttpOpenRequest**](https://msdn.microsoft.com/library/windows/desktop/aa384233)                         | [**WinHttpOpenRequest**](winhttpopenrequest.md)                                                                                                                                                       | The context value is set with [**WinHttpSendRequest**](winhttpsendrequest.md) or [**WinHttpSetOption**](winhttpsetoption.md).                                                                                                                                                                                                      |
| [**HttpQueryInfo**](https://msdn.microsoft.com/library/windows/desktop/aa384238)                             | [**WinHttpQueryHeaders**](winhttpqueryheaders.md)                                                                                                                                                     | None.                                                                                                                                                                                                                                                                                                                                |
| [**HttpSendRequest**](https://msdn.microsoft.com/library/windows/desktop/aa384247)                         | [**WinHttpSendRequest**](winhttpsendrequest.md)                                                                                                                                                       | The context value can be set with [**WinHttpSendRequest**](winhttpsendrequest.md).                                                                                                                                                                                                                                                  |
| [**HttpSendRequestEx**](https://msdn.microsoft.com/library/windows/desktop/aa384318)                     | [**WinHttpSendRequest**](winhttpsendrequest.md)                                                                                                                                                       | Buffers cannot be provided.                                                                                                                                                                                                                                                                                                          |
| [**InternetCanonicalizeUrl**](https://msdn.microsoft.com/library/windows/desktop/aa384342)         | No equivalent                                                                                                                                                                                          | URLs are now put in canonical form in [**WinHttpOpenRequest**](winhttpopenrequest.md).                                                                                                                                                                                                                                              |
| [**InternetCheckConnection**](https://msdn.microsoft.com/library/windows/desktop/aa384346)         | No equivalent                                                                                                                                                                                          | Not implemented in WinHTTP.                                                                                                                                                                                                                                                                                                          |
| [**InternetCloseHandle**](https://msdn.microsoft.com/library/windows/desktop/aa384350)                 | [**WinHttpCloseHandle**](winhttpclosehandle.md)                                                                                                                                                       | Closing a parent handle in WinHTTP does not recursively close child handles.                                                                                                                                                                                                                                                         |
| [**InternetCombineUrl**](https://msdn.microsoft.com/library/windows/desktop/aa384355)                   | No equivalent                                                                                                                                                                                          | URLs can be assembled with the [**WinHttpCreateUrl**](winhttpcreateurl.md) function.                                                                                                                                                                                                                                                |
| [**InternetConfirmZoneCrossing**](https://msdn.microsoft.com/library/windows/desktop/aa384358) | No equivalent                                                                                                                                                                                          | Not implemented in WinHTTP.                                                                                                                                                                                                                                                                                                          |
| [**InternetConnect**](https://msdn.microsoft.com/library/windows/desktop/aa384363)                         | [**WinHttpConnect**](winhttpconnect.md)                                                                                                                                                               | The context value is set with [**WinHttpSendRequest**](winhttpsendrequest.md) or [**WinHttpSetOption**](winhttpsetoption.md). Request options are set with [**WinHttpOpenRequest**](winhttpopenrequest.md). User credentials are set with [**WinHttpSetCredentials**](winhttpsetcredentials.md).                                 |
| [**InternetCrackUrl**](https://msdn.microsoft.com/library/windows/desktop/aa384376)                       | [**WinHttpCrackUrl**](winhttpcrackurl.md)                                                                                                                                                             | Opposite behavior of the ICU\_ESCAPE flag: with [**InternetCrackUrl**](https://msdn.microsoft.com/library/windows/desktop/aa384376), this flag causes escape sequences (%xx) to be converted to characters, but with [**WinHttpCrackUrl**](winhttpcrackurl.md), it causes characters that must be escaped from in an HTTP request to be converted to escape sequences. |
| [**InternetCreateUrl**](https://msdn.microsoft.com/library/windows/desktop/aa384473)                     | [**WinHttpCreateUrl**](winhttpcreateurl.md)                                                                                                                                                           | None.                                                                                                                                                                                                                                                                                                                                |
| [**InternetErrorDlg**](https://msdn.microsoft.com/library/windows/desktop/aa384694)                       | No equivalent                                                                                                                                                                                          | Because WinHTTP is targeted at server-side applications, it does not implement any user interface.                                                                                                                                                                                                                                   |
| [**InternetGetCookie**](https://msdn.microsoft.com/library/windows/desktop/aa384710)                     | No equivalent                                                                                                                                                                                          | WinHTTP does not persist data between sessions and cannot access WinINet cookies.                                                                                                                                                                                                                                                    |
| [**InternetOpen**](https://msdn.microsoft.com/library/windows/desktop/aa385096)                               | [**WinHttpOpen**](winhttpopen.md)                                                                                                                                                                     | None.                                                                                                                                                                                                                                                                                                                                |
| [**InternetOpenUrl**](https://msdn.microsoft.com/library/windows/desktop/aa385098)                         | [**WinHttpConnect**](winhttpconnect.md), [**WinHttpOpenRequest**](winhttpopenrequest.md), [**WinHttpSendRequest**](winhttpsendrequest.md), [**WinHttpReceiveResponse**](winhttpreceiveresponse.md) | This functionality is available in the WinHTTP functions listed.                                                                                                                                                                                                                                                                     |
| [**InternetQueryDataAvailable**](https://msdn.microsoft.com/library/windows/desktop/aa385100)   | [**WinHttpQueryDataAvailable**](winhttpquerydataavailable.md)                                                                                                                                         | No reserved parameters.                                                                                                                                                                                                                                                                                                              |
| [**InternetQueryOption**](https://msdn.microsoft.com/library/windows/desktop/aa385101)                 | [**WinHttpQueryOption**](winhttpqueryoption.md)                                                                                                                                                       | WinHTTP offers a different set of options from WinINet. For more information and options offered by WinHTTP, see [**Option Flags**](option-flags.md).                                                                                                                                                                               |
| [**InternetReadFile**](https://msdn.microsoft.com/library/windows/desktop/aa385103)                       | [**WinHttpReadData**](winhttpreaddata.md)                                                                                                                                                             | None.                                                                                                                                                                                                                                                                                                                                |
| [**InternetReadFileEx**](https://msdn.microsoft.com/library/windows/desktop/aa385105)                   | [**WinHttpReadData**](winhttpreaddata.md)                                                                                                                                                             | Rather than a structure, the buffer is a region of memory addressed with a pointer.                                                                                                                                                                                                                                                  |
| [**InternetSetOption**](https://msdn.microsoft.com/library/windows/desktop/aa385114)                     | [**WinHttpSetOption**](winhttpsetoption.md)                                                                                                                                                           | None.                                                                                                                                                                                                                                                                                                                                |
| [**InternetSetStatusCallback**](https://msdn.microsoft.com/library/windows/desktop/aa385120)     | [**WinHttpSetStatusCallback**](winhttpsetstatuscallback.md)                                                                                                                                           | For more information, see "Different Handling of Asynchronous Requests" in this topic.                                                                                                                                                                                                                                               |
| [**InternetTimeFromSystemTime**](https://msdn.microsoft.com/library/windows/desktop/aa385123)   | [**WinHttpTimeFromSystemTime**](winhttptimefromsystemtime.md)                                                                                                                                         | None.                                                                                                                                                                                                                                                                                                                                |
| [**InternetTimeToSystemTime**](https://msdn.microsoft.com/library/windows/desktop/aa385125)       | [**WinHttpTimeToSystemTime**](winhttptimetosystemtime.md)                                                                                                                                             | None.                                                                                                                                                                                                                                                                                                                                |
| [**InternetWriteFile**](https://msdn.microsoft.com/library/windows/desktop/aa385128)                     | [**WinHttpWriteData**](winhttpwritedata.md)                                                                                                                                                           | None.                                                                                                                                                                                                                                                                                                                                |



 

## Different Handling of Asynchronous Requests

Be aware that in WinINet and WinHTTP, some functions can complete asynchronous requests either synchronously or asynchronously. Your application must handle either situation. There are significant differences in how WinINet and WinHTTP handle these potentially asynchronous functions.

WinINet

-   Synchronous completion: If a potentially asynchronous WinINet function call completes synchronously, the OUT parameters of the function return the results of the operation. When an error occurs, retrieve the error code by calling [**GetLastError**](https://msdn.microsoft.com/library/windows/desktop/ms679360) after the WinINet function call.

-   Asynchronous completion: If a potentially asynchronous function call completes asynchronously, the results of the operation, and any errors, are accessible in the callback function. The callback function is executed on a worker thread, not on the thread that made the initial function call.

In other words, your application must duplicate logic to handle the results of such operations in two places: both immediately after the function call and in the callback function.

WinHTTP simplifies this model by enabling you to implement the operational logic only in the callback function, which receives a completion notification regardless of whether the operation completed synchronously or asynchronously. When asynchronous operation is enabled, the OUT parameters of WinHTTP functions do not return meaningful data and must be set to **NULL**.

The only significant difference between asynchronous and synchronous completion in WinHTTP, from the application perspective, is in where the callback function is executed.

WinHTTP

-   Synchronous completion: When an operation completes synchronously, the results are returned in a callback function that executes in the same thread as the original function call.

-   Asynchronous completion: When an operation completes asynchronously, the results are returned in a callback function that executes in a worker thread.

Although most errors can also be handled entirely within the callback function, WinHTTP applications must still be prepared for a function to return **FALSE** because of an ERROR\_INVALID\_PARAMETER or other similar error retrieved by calling [**GetLastError**](https://msdn.microsoft.com/library/windows/desktop/ms679360).

Unlike WinINet, which can execute multiple asynchronous operations simultaneously, WinHTTP enforces a policy of one pending asynchronous operation per request handle. If one operation is pending and another WinHTTP function is called, the second function fails and [**GetLastError**](https://msdn.microsoft.com/library/windows/desktop/ms679360) returns ERROR\_INVALID\_OPERATION.

WinHTTP simplifies this model by enabling you to implement the operational logic only in the callback function, which receives a completion notification regardless of whether the operation completed synchronously or asynchronously. When asynchronous operation is enabled, the OUT parameters of WinHTTP functions do not return meaningful data and must be set to **NULL**.

## Differences in WinHTTP Callback Notifications

The status callback function receives updates on the status of operations through notification flags. In WinHTTP, notifications are selected using the *dwNotificationFlags* parameter of the [**WinHttpSetStatusCallback**](winhttpsetstatuscallback.md) function. Use the **WINHTTP\_CALLBACK\_FLAG\_ALL\_NOTIFICATIONS** flag to be notified of all status updates.

Notifications that indicate a particular operation is complete are called completion notifications, or just completions. In WinINet, each time the callback function receives a completion, the *lpvStatusInformation* parameter contains an [**INTERNET\_ASYNC\_RESULT**](https://msdn.microsoft.com/library/windows/desktop/aa385129) structure. In WinHTTP, this structure is not available for all completions. It is important to review the reference page for [**WINHTTP\_STATUS\_CALLBACK**](internet-status-callback-prototype.md), which contains information about notifications and what type of data can be expected for each.

In WinHTTP, a single completion, **WINHTTP\_CALLBACK\_STATUS\_REQUEST\_ERROR**, indicates that an operation failed. All other completions indicate a successful operation.

Both WinINet and WinHTTP use a user-defined context value to pass information from the main thread to the status callback function, which can be executed on a worker thread. In WinINet, the context value used by the status callback function is set by calling one of several functions. In WinHTTP, the context value is set only with [**WinHttpSendRequest**](winhttpsendrequest.md) or [**WinHttpSetOption**](winhttpsetoption.md). Because of this, it is possible in WinHTTP for a notification to occur before a context value is set. If the callback function receives a notification before the context value is set, the application must be prepared to receive **NULL** in the *dwContext* parameter of the callback function.

## Authentication Differences

In WinINet, user credentials are set by calling the [**InternetSetOption**](https://msdn.microsoft.com/library/windows/desktop/aa385114) function, using code similar to that provided in the following code example.

``` syntax
// Use the WinINet InternetSetOption function to set the 
// user credentials to the user name contained in strUsername 
// and the password to the contents of strPassword.
       
InternetSetOption( hRequest, INTERNET_OPTION_PROXY_USERNAME, 
                   strUsername, strlen(strUsername) + 1 );

InternetSetOption( hRequest, INTERNET_OPTION_PROXY_PASSWORD, 
                   strPassword, strlen(strPassword) + 1 );
```

For compatibility, user credentials can similarly be set in WinHTTP using the [**WinHttpSetOption**](winhttpsetoption.md) function, but this is not recommended because it can pose a security vulnerability.

Instead, when an application receives a 401 status code in WinHTTP, the recommended method of setting credentials is first to identify an authentication scheme using [**WinHttpQueryAuthSchemes**](winhttpqueryauthschemes.md) and, second, set the credentials using [**WinHttpSetCredentials**](winhttpsetcredentials.md). The following code example shows how to do this.

``` syntax
DWORD dwSupportedSchemes;
DWORD dwPrefered;
DWORD dwTarget;

// Obtain the supported and first schemes.
WinHttpQueryAuthSchemes( hRequest, &dwSupportedSchemes, &dwPrefered, &dwTarget );

// Set the credentials before resending the request.
WinHttpSetCredentials( hRequest, dwTarget, dwPrefered, strUsername, strPassword, NULL );
```

Because there is no equivalent to [**InternetErrorDlg**](https://msdn.microsoft.com/library/windows/desktop/aa384694) in WinHTTP, applications that obtain credentials through a user interface must provide their own interface.

Unlike WinINet, WinHTTP does not cache passwords. Valid user credentials must be supplied for each request.

WinHTTP does not support the Distributed Password Authentication (DPA) scheme supported by WinINet. WinHTTP does, however, support Microsoft Passport 1.4. For more information about using Passport authentication in WinHTTP, see [Passport Authentication in WinHTTP](passport-authentication-in-winhttp.md).

WinHTTP does not rely on Internet Explorer settings to determine the automatic logon policy. Instead, the auto-logon policy is set with [**WinHttpSetOption**](winhttpsetoption.md). For more information about authentication in WinHTTP, including the auto-logon policy, see [Authentication in WinHTTP](authentication-in-winhttp.md).

## Differences in Secure HTTP Transactions

In WinINet, initiate a secure session using either [**HttpOpenRequest**](https://msdn.microsoft.com/library/windows/desktop/aa384233) or [**InternetConnect**](https://msdn.microsoft.com/library/windows/desktop/aa384363), but in WinHTTP, you must call [**WinHttpOpenRequest**](winhttpopenrequest.md) using the **WINHTTP\_FLAG\_SECURE** flag.

In a secure HTTP transaction, server certificates can be used to authenticate a server to the client. In WinINet, if a server certificate contains errors, [**HttpSendRequest**](https://msdn.microsoft.com/library/windows/desktop/aa384247) fails and provides details about the certificate errors.

In WinHttp, server certificate errors are handled according to the version as follows:

-   Starting with WinHttp 5.1, if a server certificate fails or contains errors, the call to [**WinHttpSendRequest**](winhttpsendrequest.md) reports a **WINHTTP\_CALLBACK\_STATUS\_SECURE\_FAILURE** in the callback function. If the error generated by **WinHttpSendRequest** is ignored, subsequent calls to [**WinHttpReceiveResponse**](winhttpreceiveresponse.md) fail with an ERROR\_WINHTTP\_OPERATION\_CANCELLED error.
-   In WinHTTP 5.0, errors in server certificates do not, by default, cause a request to fail. Instead, the errors are reported in the callback function with the **WINHTTP\_CALLBACK\_STATUS\_SECURE\_FAILURE** notification.

On some earlier platforms, WinINet supported the Private Communication Technology (PCT) and/or Fortezza protocols, although not on Windows XP.

WinHTTP does not support the PCT and Fortezza protocols on any platform, and instead relies on Secure Sockets Layer (SSL) 2.0, SSL 3.0, or Transport Layer Security (TLS) 1.0.

 

 


