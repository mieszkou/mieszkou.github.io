---
title: "Powershell: podniesienie uprawnień i wykonanie polecenia"
description: ""
date: 2023-05-22
image: /img/2023-02-12-23-33-57.png
hidden: false
comments: true
draft: false
tags:
    - powershell
    - oneliner
    - server
    - windowsserver
categories:
    - Powershell
---


```powershell
# Podniesienie uprawnień do trybu administratora
    Start-Process powershell.exe -Verb RunAs -ArgumentList "-NoProfile -ExecutionPolicy Bypass -Command `"& {Install-Module -Name AzureAD -Force -AllowClobber}`""
```
