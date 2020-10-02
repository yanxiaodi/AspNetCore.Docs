---
title: Get started with HTTP/3 and Kestrel
author: rick-anderson
description: Learn about Kestrel, the cross-platform web server for ASP.NET Core.
monikerRange: '>= aspnetcore-5.0'
ms.author: jkotalik
ms.custom: mvc
ms.date: 10/02/2020
no-loc: ["ASP.NET Core Identity", cookie, Cookie, Blazor, "Blazor Server", "Blazor WebAssembly", "Identity", "Let's Encrypt", Razor, SignalR]
uid: fundamentals/servers/kestrel/http3
---
# Get started with HTTP/3 and Kestrel

HTTP/3 is a new protocol to exchange information over the web. Notably, HTTP/3 uses UDP instead of TCP to transfer information across the internet. QUIC is built on top of UDP to handle many of the things TCP handled before, including  

! NOTE, HTTP/3 in .NET 5 is still in experimental preview. Do not host ANY production sites with HTTP/3 with .NET 5. This guide is purely for try out HTTP/3 locally or in test environments.

## Prerequisites

### Windows

1. Download the latest 5.0 build of .NET from <https://github.com/dotnet/installer>. Download the 5.0.100 RC1 branch.
2. Latest [Windows Insider Builds](https://insider.windows.com/en-us/), Insiders Fast build. This is required for Schannel support for QUIC.
    To confirm you have a new enough build, run winver on command line and confirm you version is greater than Version 2004 (OS Build 20145.1000)
3. Enabling TLS 1.3. Add the following registry keys to enable TLS 1.3.

    ```text
    reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.3\Server" /v DisabledByDefault /t REG_DWORD /d 0 /f
    reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.3\Server" /v Enabled /t REG_DWORD /d 1 /f
    reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.3\Client" /v DisabledByDefault /t REG_DWORD /d 0 /f
    reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.3\Client" /v Enabled /t REG_DWORD /d 1 /f
    ```
### Linux


## Sending a request with HTTP/3 on your browser

1. Download Edge Dev or Canary <https://www.microsoftedgeinsider.com/en-us/download.>
2. Either launch edge on the command line with
   ```text
    & "C:\Users\<user>\AppData\Local\Microsoft\Edge SxS\Application\msedge.exe" --enable-quic --quic-version=h3-29 --origin-to-force-quic-on=localhost:5557
   ```
   or adding the flags to the Microsoft Edge Dev Properties Target.
3. Hit localhost:5557 from the browser, check the network tab, the request should be HTTP/3 with the spec h3-29.

## Sending a request with HttpClient