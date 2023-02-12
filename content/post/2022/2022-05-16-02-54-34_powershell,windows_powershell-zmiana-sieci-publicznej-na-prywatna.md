---
title: "PowerShell: Zmiana sieci publicznej na prywatną"
description: 
date: 2022-05-16
image: /img/2023-02-12-23-33-57.png
hidden: false
comments: true
draft: false
tags:
    - powershell
    - windows
categories:
    - PowerShell
---

Zmiana sieci publicznej na prywatną

`Ethernet` to nazwa połączenia sieciowego.

```
Set-NetConnectionProfile -InterfaceAlias "Ethernet" -NetworkCategory Private
```