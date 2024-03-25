---
title: "Pobierz i uruchom plik jednym poleceniem"
description: "Powershell - Pobierz i uruchom plik jednym poleceniem / Download the executable file and run it with single command"
date: 2024-03-25T15:41:31+01:00
image: 
hidden: false
comments: true
draft: false
tags:
    - powershell
    - windows
    - oneliner
categories:
    - PowerShell
    - Administracja
---

Jak pobrać plik z internetu i go uruchomić?

Może tak: 

Skopiuj do schowka:
```powershell
$u="https://urbanowski.info/pub/PCM_7_8_128_147_Fa_z_komentarzem_20240325.exe"
$f=$u -replace '^.*/(.*/.*)$','$1'
$s=$env:TEMP\$f
$ProgressPreference='SilentlyContinue'
[Net.ServicePointManager]::SecurityProtocol='Tls12'
iwr $u -OutFile (New-Item -Path $s -Force)
Start $s
```

To samo w jednym wierszu:
Skopiuj do schowka:
```powershell
$u="https://urbanowski.info/pub/PCM_7_8_128_147_Fa_z_komentarzem_20240325.exe";$f=$u -replace '^.*/(.*/.*)$','$1';$s=$env:TEMP\$f;$ProgressPreference='SilentlyContinue';[Net.ServicePointManager]::SecurityProtocol='Tls12';iwr $u -OutFile (New-Item -Path $s -Force);Start $s
```

Włącz okno PowerShell np.: <kbd>⌘ Win</kbd> + <kbd>x</kbd> -> <kbd>i</kbd> -> <kbd>Ctrl</kbd> + <kbd>v</kbd> -> <kbd>Enter</kbd> i gotowe

