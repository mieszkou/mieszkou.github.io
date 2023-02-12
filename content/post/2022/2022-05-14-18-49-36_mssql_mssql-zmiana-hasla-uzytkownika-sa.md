---
title: "MSSQL - zmiana hasła użytkownika sa"
description: 
date: 2022-05-14
image: 
hidden: false
comments: true
draft: false
tags:
    - mssql
    - sql
categories:
    - SQL
    - MSSQL
    - Administracja
---

Jeśli nie znam hasła użytkownika `sa`, ale mam dostęp do konta windows z uprawnieniami do serwera SQL (najczęściej użytkownik który instalował instancję SQL) możemy zmienić hasło użytkownika `sa`.

W tym celu łączę się z serwerem SQL:

```
osql -S SERWERSQL –E
```
 po połączeniu zmieniamy hasło:
```sql
sp_password 'Wapro3000',’noweHasl0’
go
-- lub tak:
ALTER LOGIN sa WITH PASSWORD = 'noweHasl0'
go
```