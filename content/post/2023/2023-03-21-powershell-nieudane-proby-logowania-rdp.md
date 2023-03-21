---
title: "Powershell: nieudane próby logowania"
description: "Podsumowane ilości nieudanych prób logowania w kolejnych dniach"
date: 2023-03-21
image: 
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

Aby policzyć nieudane próby logowania w kolejnych dniach za pomocą PowerShell, można użyć następującej komendy:

```powershell
Get-EventLog -LogName Security | Where-Object {$_.EventID -eq 4625} | Group-Object -Property {$_.TimeGenerated.ToShortDateString()} | Select-Object Name, Count
```

Powyższe polecenie pobiera dziennik zdarzeń bezpieczeństwa, filtruje tylko te wpisy, które mają identyfikator zdarzenia 4625 (co odpowiada nieudanej próbie logowania), grupuje je według daty (za pomocą właściwości TimeGenerated), a następnie zwraca nazwę grupy (czyli datę) oraz liczbę wpisów w grupie (czyli liczbę nieudanych prób logowania w danym dniu).