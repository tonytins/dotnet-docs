---
title: SYSLIB0014 warning
description: Learn about the System.Net obsoletions that generate compile-time warning SYSLIB0014.
ms.topic: reference
ms.date: 04/24/2021
---
# SYSLIB0014: WebRequest, HttpWebRequest, ServicePoint, WebClient are obsolete

The following APIs are marked as obsolete, starting in .NET 6. Using them in code generates warning `SYSLIB0014` at compile time.

- <xref:System.Net.WebRequest?displayProperty=fullName>
- <xref:System.Net.HttpWebRequest?displayProperty=fullName>
- <xref:System.Net.ServicePoint?displayProperty=fullName>
- <xref:System.Net.WebClient?displayProperty=fullName>

## Workarounds

Use <xref:System.Net.Http.HttpClient> instead.

[!INCLUDE [suppress-syslib-warning](../../../../includes/suppress-syslib-warning.md)]

## See also

- [WebRequest, WebClient, and ServicePoint are obsolete](../networking/6.0/webrequest-deprecated.md)
