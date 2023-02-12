---
title: "Windows 10: błędy touchpada i zrzuty log-a"
description: 
date: 2022-05-16
image: 
hidden: false
comments: true
draft: false
tags:
    - windows
categories:
    - Windows
    - Administracja
---

Błędy Touchpada i zrzuty log - wyłączenie

```
reg add HKEY_LOCAL_MACHINESYSTEMCurrentControlSetservicesSynTPParametersDebug /v DumpKernel /d 00000000 /t REG_DWORD /f
```