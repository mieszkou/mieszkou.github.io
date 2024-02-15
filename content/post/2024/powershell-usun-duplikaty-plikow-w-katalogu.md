---
title: "Powershell - kasowanie duplikatów plików w katalogu"
description: "Powershell - kasowanie duplikatów plików w katalogu"
date: 2024-02-15T11:42:46+01:00
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
---

```powershell
Get-ChildItem -Path . -File -Recurse | ForEach-Object {
    [PSCustomObject]@{
        Path = $_.FullName
        Hash = Get-FileHash -Path $_.FullName -Algorithm SHA256 | Select-Object -ExpandProperty Hash
        LastWriteTime = $_.LastWriteTime
    }
} | Group-Object -Property Hash | ForEach-Object {
    $_.Group | Sort-Object LastWriteTime -Descending | Select-Object -Skip 1
} | Remove-Item -Force
```