---
title: "Nmap: podstawy"
description: 
date: 2022-05-16
image: 
hidden: false
comments: true
draft: false
tags:
    - nmap
    - lan
    - sieci
categories:
    - Programy których używam
    - Sieci
---

Skanowanie sieci:
```
nmap -sn 192.168.88.0/24
```

Skanowanie portow TCP:
```
nmap -sT 192.168.88.0/24
```

Skanowanie portow UDP:
```
nmap -sU 192.168.88.0/24
```