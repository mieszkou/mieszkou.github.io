---
title: "Windows Terminal - split and run"
description: 
date: 2023-10-18
hidden: false
comments: true
draft: false
tags:
    - windows
    - powershell
categories:
    - Powershell
---

Kasowanie logów kas

```bash
wt -M -d "./" ping wp.pl -t; ^
sp -V -d "./" ping wp.pl -t; ^
mf left; ^
sp -H -d "./" ping wp.pl -t; ^
mf right; ^
sp -H -d "./" ping wp.pl -t
```