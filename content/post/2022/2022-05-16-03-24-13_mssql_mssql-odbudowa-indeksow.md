---
title: "MSSQL: Odbudowa indeksów"
description: 
date: 2022-05-14
image: 
hidden: false
comments: true
draft: false
tags:
    - mssql
categories:
    - MSSQL
    - Administracja
---

Odbudowa indeksów dla wszystkich tabel w bazie danych:

```
GO
EXEC sp_MSforeachtable @command1="print '?' DBCC DBREINDEX ('?', ' ', 80)"
GO
```