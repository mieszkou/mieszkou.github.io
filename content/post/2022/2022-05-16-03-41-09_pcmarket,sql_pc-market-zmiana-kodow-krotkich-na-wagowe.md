---
title: "PC-Market: zmiana kodów krótkich na wagowe"
description: 
date: 2022-05-16
image: /img/2023-02-12-23-08-32.png
hidden: false
comments: true
draft: false
tags:
    - insoft
    - pcmarket
    - sql
categories:
    - Insoft
---

PC-Market: zmiana kodów krótkich na wagowe

```sql
Select * from Towar where kod like '29%'

Select getdate(), '29' + right('0000' + kod, 4) + '???????', * from Towar where JMid = 2 AND len(kod) <=4 order by kod

UPDATE Towar set kod = '29' + right('0000' + kod, 4) + '???????', zmiana = getdate(), zmianaistotna = getdate() where JMid = 2 AND len(kod) <=4 

-- AND asid not in(134,132)
```

lub tak:

```sql
UPDATE [dbo].[Towar]
   SET [Kod] = cast(290000 + cast(kod as int) as varchar) + '???????'
   WHERE Towid < 10
GO

select * from towar where towid < 50
```
