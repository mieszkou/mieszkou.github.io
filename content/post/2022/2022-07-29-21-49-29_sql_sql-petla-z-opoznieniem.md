---
title: "SQL: pętla z opóźnieniem"
description: 
date: 2022-07-29
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
---


```sql
--CREATE 5 RANDOM ORDERS BY CUSTOMER ID 4, MONITOR FOR ALERTS IN SLACK.
WHILE (@I < 5)
BEGIN
   SET @M = (SELECT ROUND(RAND() * 12, 0))
   SET @D = (SELECT ROUND(RAND() * 28, 0))
   SET @Y = (SELECT 2020)
   SET @DT = (SELECT CAST(@M AS VARCHAR(2)) + '/' + CAST(@D AS VARCHAR(2)) + '/' + CAST(@Y AS VARCHAR(4)))
   SET @AMT = (SELECT 1 + ROUND(RAND() * (600 + 1 - 1), 0))
 
   INSERT INTO Orders
   VALUES(@DT,@AMT,'Random',4)
 
   SET @I = @I + 1
   WAITFOR DELAY '00:00:05'
END
```