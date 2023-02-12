---
title: "WinSCP synchronizacja katalogów"
description: 
date: 2022-05-16
image: 
hidden: false
comments: true
draft: false
tags:
    - ftp
    - winscp
categories:
    - Programy których używam
---

Synchronizacja lokalnego katalogu z serwerem ftp przy użyciu WinSCP, z pominięciem katalogu `.git`

Tworze sobie 2 pliki

make.cmd:
```
WinSCP.com /script=make.txt
```

make.txt:
```
option batch abort
option confirm off
open ftp://login:haslo@ftp.host.pl
synchronize remote ".folder" "/folder/na/ftp/" -filemask="|.git;*/input/*;*/output/*"
close
exit
```

