---
title: "Powershell: nieudane próby logowania"
description: "Podsumowane ilości nieudanych prób logowania w kolejnych dniach"
date: 2023-03-21
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

Aby policzyć nieudane próby logowania w kolejnych dniach za pomocą PowerShell, można użyć następującej komendy:

```powershell
Get-EventLog -LogName Security | Where-Object {$_.EventID -eq 4625} | Group-Object -Property {$_.TimeGenerated.ToShortDateString()} | Select-Object Name, Count
```

Powyższe polecenie pobiera dziennik zdarzeń bezpieczeństwa, filtruje tylko te wpisy, które mają identyfikator zdarzenia 4625 (co odpowiada nieudanej próbie logowania), grupuje je według daty (za pomocą właściwości TimeGenerated), a następnie zwraca nazwę grupy (czyli datę) oraz liczbę wpisów w grupie (czyli liczbę nieudanych prób logowania w danym dniu).

## Start/restart uruchamianie systemu

https://serverfault.com/questions/401961/event-log-time-when-computer-start-up-boot-up

EventViewer ( System Log )
6009 and 6005 same time stamp, system just started.
6013 - system has been up for a day or more, time in seconds.
6006 - the system was rebooted or shutdown.

> This answer is no longer complete because in Windows 10, events 6009 and 6005 are not always logged if a user clicks "Shut Down" from the Start Menu and then turns on the computer by pressing the power button.

PowerShell: Get All Reboot Messages in the Last Month

```
Get-EventLog -LogName System -After $(Get-Date).AddMonths(-1) | Where { 6009,6005,6006 -contains $_.EventID}
```