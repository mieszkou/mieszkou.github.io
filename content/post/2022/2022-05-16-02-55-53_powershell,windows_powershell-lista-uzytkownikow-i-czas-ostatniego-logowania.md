---
title: "PowerShell: Lista użytkowników i czas ostatniego logowania"
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


Lista użytkowników i czas ostatniego logowania:

```
get-aduser -f * -pr lastlogondate|sort -property lastlogondate|ft samaccountname,lastlogondate -auto
```