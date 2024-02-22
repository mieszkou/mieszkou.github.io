---
title: "Reset stosu tcp windows" 
description: "Reset_stosu_tcp_windows"
date: 2024-02-22T16:19:02+01:00
image: 
hidden: false
comments: true
draft: false
tags:
    - windows
categories:
    - Administracja
---

Reset stosu TCP, pomaga często na problemy z połączeniem VPN. Polecenia w oknie z uprawnieniami administratora.

```
netsh int ip reset
netsh int ipv4 reset
netsh int ipv6 reset
``` 


Potem restart komputera.
