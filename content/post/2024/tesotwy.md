---
title: "TESTOsfdgfdg dWY"
description: "Teściki"
date: 2024-10-30
image: 
hidden: false
comments: true
draft: false
tags:
    - test
categories:
    - TEST
---

sdfg sdfgsdfsdfg dsfg
 sdfg sdfgsdfg sdfg sdfg
 sdf gsdgf sdgfsdfgsdfg
 dsgf 

 sf sdfg sdfgsf d

 -sdfg sdfg sdfg fsdg
 - sdfgsdfgdsgf sdgfs
 - - sdfgsdgf sdgfsdgf
 - dsgf sdgf sdgf sdfg
 - s dfgsdgfs d


# testty

```
- [ ]  sdfgsdfg sdgf
- [ ] dsfghdsgdfg

```


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