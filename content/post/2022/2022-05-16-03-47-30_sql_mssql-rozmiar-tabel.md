---
title: "MSSQL - rozmiar tabel"
description: 
date: 2022-05-16
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


MSSQL - rozmiar tabel

```
SELECT 
    DF.name as [Plik]
    --,[File_Location] = DF.PHYSICAL_NAME
    ,[Rozmiar (MB)] = CONVERT(DECIMAL(10,2),DF.SIZE/128.0)
    ,[Uzyte (MB)] = CONVERT(DECIMAL(10,2),DF.SIZE/128.0 - ((SIZE/128.0) - CAST(FILEPROPERTY(DF.NAME, 'SPACEUSED') AS INT)/128.0))
    ,[Wolne (MB)] = CONVERT(DECIMAL(10,2),DF.SIZE/128.0 - CAST(FILEPROPERTY(DF.NAME, 'SPACEUSED') AS INT)/128.0)
    ,[Wolne (%)] = CONVERT(DECIMAL(10,2),((DF.SIZE/128.0 - CAST(FILEPROPERTY(DF.NAME, 'SPACEUSED') AS INT)/128.0)/(DF.SIZE/128.0))*100)
FROM sys.database_files DF
LEFT JOIN sys.filegroups FG
ON DF.data_space_id = FG.data_space_id 
```

```
SELECT
-- s.Name AS SchemaName,
t.Name AS [Tabela],
p.rows AS [Ilość rekordów],
CAST(ROUND((SUM(a.total_pages) / 128.00), 2) AS NUMERIC(36, 2)) AS [Rozmiar (MB)],
CAST(ROUND((SUM(a.used_pages) / 128.00), 2) AS NUMERIC(36, 2)) AS [Uzyte (MB)],
CAST(ROUND((SUM(a.total_pages) - SUM(a.used_pages)) / 128.00, 2) AS NUMERIC(36, 2)) AS [Wolne (MB)]
FROM sys.tables t
INNER JOIN sys.indexes i ON t.OBJECT_ID = i.object_id
INNER JOIN sys.partitions p ON i.object_id = p.OBJECT_ID AND i.index_id = p.index_id
INNER JOIN sys.allocation_units a ON p.partition_id = a.container_id
INNER JOIN sys.schemas s ON t.schema_id = s.schema_id
GROUP BY t.Name, s.Name, p.Rows
ORDER BY [Rozmiar (MB)] DESC
GO
```