---
title: "PowerShell: Reset uprawnień do wszystkich plików i katalogów"
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

Reset uprawnień do wszystkich plików i katalogów:

```
icacls * /q /c /t /reset
```