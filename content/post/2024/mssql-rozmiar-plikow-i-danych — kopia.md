---
title: "MSSQL Rozmiar plików i danych"
description: "Mssql Rozmiar Plikow I Danych"
date: 2024-03-30T17:07:48+01:00
image: 
hidden: false
comments: true
draft: false
tags:
    - sql
    - mssql
categories:
    - MSSQL
---

```sql
select
a.FILEID,
[FILE_SIZE_MB] = 
convert(decimal(12,2),round(a.size/128.000,2)),
[SPACE_USED_MB] =
convert(decimal(12,2),round(fileproperty(a.name, 'SpaceUsed')/128.000,2)),
[FREE_SPACE_MB] =
convert(decimal(12,2),round((a.size-fileproperty(a.name, 'SpaceUsed'))/128.000,2)) ,
NAME = left(a.NAME,15),
FILENAME = left(a.FILENAME,30)
from
dbo.sysfiles a
```