---
title: "PC-Market - kasowanie logów kas"
description: 
date: 2023-10-18
image: /img/2023-02-12-23-08-32.png
hidden: false
comments: true
draft: false
tags:
    - insoft
    - pcmarket
categories:
    - Insoft
---

Kasowanie logów kas

```bash
forfiles /S /D -14 /M NEO_LOG*.TXT /C "cmd /c echo @path & del @path"
rem forfiles /S /M ARCH2.EXP /C "cmd /c echo @path & del @path"
pause
```

![](assets/2024-02-03-12-05-55.png)