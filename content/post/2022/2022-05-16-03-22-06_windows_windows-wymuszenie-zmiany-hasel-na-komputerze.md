---
title: "Windows: Wymuszenie zmiany haseł na komputerze"
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


Poniższe komendy należy wykonać w wierszu poleceń uruchomionym jako Administrator

```
net accounts /MAXPWAGE:30 
net accounts /MINPWLEN:8 
net accounts /UNIQUEPW:12 
wmic path Win32_UserAccount set PasswordExpires=True
```
