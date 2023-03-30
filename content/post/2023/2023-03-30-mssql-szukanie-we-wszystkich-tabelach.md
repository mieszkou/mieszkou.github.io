---
title: "MSSQL: Szukanie ciągu znaków we wszystkich tabelach"
description: "Szukanie ciągu znaków we wszystkich tabelach"
date: 2023-03-30
image: 
hidden: false
comments: true
draft: false
tags:
    - mssql
    - sql
categories:
    - MSSQL
    - Administracja
---

- https://stackoverflow.com/questions/15757263/find-a-string-by-searching-all-tables-in-sql-server

## Szukanie ciągu znaków we wszystkich tabelach (dla sqlsrv < 2016)

```sql
DECLARE
@search_string  VARCHAR(100),
@table_name     SYSNAME,
@table_id       INT,
@column_name    SYSNAME,
@sql_string     VARCHAR(2000)

SET @search_string = 'STRING'

DECLARE tables_cur CURSOR FOR SELECT ss.name +'.'+ so.name [name], object_id FROM sys.objects so INNER JOIN sys.schemas ss ON so.schema_id = ss.schema_id WHERE  type = 'U'

OPEN tables_cur

FETCH NEXT FROM tables_cur INTO @table_name, @table_id

WHILE (@@FETCH_STATUS = 0)
BEGIN
    DECLARE columns_cur CURSOR FOR SELECT name FROM sys.columns WHERE object_id = @table_id 
        AND system_type_id IN (167, 175, 231, 239)

    OPEN columns_cur

    FETCH NEXT FROM columns_cur INTO @column_name
        WHILE (@@FETCH_STATUS = 0)
        BEGIN
            SET @sql_string = 'IF EXISTS (SELECT * FROM ' + @table_name + ' WHERE [' + @column_name + '] 
            LIKE ''%' + @search_string + '%'') PRINT ''' + @table_name + ', ' + @column_name + ''''

            EXECUTE(@sql_string)

        FETCH NEXT FROM columns_cur INTO @column_name
        END

    CLOSE columns_cur

DEALLOCATE columns_cur

FETCH NEXT FROM tables_cur INTO @table_name, @table_id
END

CLOSE tables_cur
DEALLOCATE tables_cur

```

## Szukanie ciągu znaków we wszystkich tabelach (dla sqlsrv >= 2016)

> nie testowałem

```sql
--=======================================================================
--  MSSQL Unified Search
--  Minimum compatibility level = 130 (SQL Server 2016)
--      NOTE: The minimum compatibility level is required by the built-in STRING_SPLIT() function.
--          However, you can create the STRING_SPLIT() function at the bottom of this script for
--          lower versions of MSSQL Server.
--
--  Usage:
--      Set the parameters below and execute this script.
--
/************************ Enter Parameters Here ************************/
/**/
/**/    DECLARE @SearchString VARCHAR(1000) = 'string to search for';  -- Accepts SQL wilcards
/**/
/**/    DECLARE @IncludeUserTables BIT = 1;
/**/    DECLARE @IncludeViews BIT = 0;
/**/    DECLARE @IncludeStoredProcedures BIT = 0;
/**/    DECLARE @IncludeFunctions BIT = 0;
/**/    DECLARE @IncludeTriggers BIT = 0;
/**/
/**/    DECLARE @DebugMode BIT = 0;
/**/    DECLARE @ExcludeColumnTypes NVARCHAR(500) = 'text, ntext, char, nchar, timestamp, bigint, tinyint, smallint, bit, date, time, smalldatetime, datetime, datetime2, real, money, float, decimal, binary, varbinary, image';  -- Comma delimited list
/**/
/***********************************************************************/


SET NOCOUNT ON;
SET @SearchString = QUOTENAME(@SearchString,'''');

DECLARE @Results TABLE ([ObjectType] NVARCHAR(200), [ObjectName] NVARCHAR(200), [ColumnName] NVARCHAR(400), [Value] NVARCHAR(MAX), [SelectStatement] NVARCHAR(1000));
DECLARE @ExcludeColTypes TABLE (system_type_id INT);

INSERT INTO @ExcludeColTypes ([system_type_id])
    SELECT [system_type_id]
    FROM sys.types WHERE
    [name] IN (
        SELECT LTRIM(RTRIM([value])) FROM STRING_SPLIT(@ExcludeColumnTypes,',')
        );

DECLARE @ObjectType NVARCHAR(200);
DECLARE @ObjectName NVARCHAR(200);
DECLARE @Value NVARCHAR(MAX);
DECLARE @SelectStatement NVARCHAR(1000);
DECLARE @Query NVARCHAR(4000);


/********************* Table Objects *********************/
IF (@IncludeUserTables = 1)
BEGIN
    DECLARE @TableObjectId INT = (SELECT MIN([object_id]) FROM sys.tables);
    DECLARE @ColumnId INT;
    WHILE @TableObjectId IS NOT NULL
    BEGIN
    
        SELECT @ObjectType = 'USER TABLE';
        SELECT @ObjectName = '[' + SCHEMA_NAME([schema_id]) + '].[' + OBJECT_NAME(@TableObjectId) + ']' FROM sys.tables WHERE [object_id] = @TableObjectId;

        SET @ColumnId = (SELECT MIN([column_id]) FROM sys.columns WHERE [system_type_id] NOT IN (SELECT [system_type_id] FROM @ExcludeColTypes) AND [object_id] = @TableObjectId);
        WHILE @ColumnId IS NOT NULL
        BEGIN

            SELECT @Value = '[' + [name] +']' FROM sys.columns WHERE [object_id] = @TableObjectId AND column_id = @ColumnId;

            SET @SelectStatement = 'SELECT * FROM ' + @ObjectName + ' WHERE CAST(' + @Value + ' AS NVARCHAR(4000)) LIKE ' + @SearchString + ';';

            SET @Query = 'SELECT '
                + QUOTENAME(@ObjectType, '''')
                + ', ' + QUOTENAME(@ObjectName, '''')
                + ', ' + QUOTENAME(@Value, '''')
                + ', ' + @Value
                + ', ''' + REPLACE(@SelectStatement,'''','''''') + ''''
                + ' FROM ' + @ObjectName
                + ' WHERE CAST(' + @Value + ' AS NVARCHAR(4000)) LIKE ' + @SearchString + ';';

            IF @DebugMode = 0
            BEGIN
                INSERT INTO @Results EXEC(@Query);
            END;
            ELSE
            BEGIN
                PRINT 'Select Statement:  ' + @SelectStatement;
                PRINT 'Query:  ' + @Query;
            END;

            SET @ColumnId = (SELECT MIN([column_id]) FROM sys.columns WHERE [system_type_id] NOT IN (SELECT [system_type_id] FROM @ExcludeColTypes) AND [object_id] = @TableObjectId AND [column_id] > @ColumnId);
        END;

        SET @TableObjectId = (SELECT MIN([object_id]) FROM sys.tables WHERE [object_id] > @TableObjectId);
    END;
END;

/********************* Objects Other than Tables *********************/
SET @Query = 'SELECT ' +
    'ObjectType = CASE ' +
        'WHEN b.[type] = ''V'' THEN ''VIEW'' ' +
        'WHEN b.[type] = ''P'' THEN ''STORED PROCEDURE'' ' +
        'WHEN b.[type] = ''FN'' THEN ''SCALAR-VALUED FUNCTION'' ' +
        'WHEN b.[type] = ''IF'' THEN ''TABLE-VALUED FUNCTION'' ' +
        'WHEN b.[type] = ''TR'' THEN ''TRIGGER'' ' +
    'END ' +
    ',[ObjectName] = ''['' + SCHEMA_NAME(b.[schema_id]) + ''].['' + OBJECT_NAME(a.[object_id]) + '']'' ' +
    ',[ColumnName] = NULL ' +
    ',[Value] = a.[definition] ' +
    ',[SelectStatement] = ''SP_HELPTEXT '' + QUOTENAME(''['' + SCHEMA_NAME(b.[schema_id]) + ''].['' + OBJECT_NAME(a.[object_id]) + '']'','''''''') + '';'' ' +
'FROM [sys].[sql_modules] a ' +
'JOIN [sys].[objects] b ON a.[object_id] = b.[object_id] ' +
'WHERE ' +
    '( ' +
    '   a.[definition] LIKE ' + @SearchString + 
    ') ' +
    'AND ' +
    '( ' +
    '   ( ' +
            CAST(@IncludeViews AS VARCHAR(1)) + ' = 1 ' +
    '       AND ' +
    '       b.[type] IN (''V'') ' +
    '   ) ' +
    '   OR ' +
    '   ( ' +
            CAST(@IncludeStoredProcedures AS VARCHAR(1)) + ' = 1 ' +
    '       AND ' +
    '       b.[type] IN (''P'') ' +
    '   ) ' +
    '   OR ' +
    '   ( ' +
            CAST(@IncludeFunctions AS VARCHAR(1)) + ' = 1 ' +
    '       AND ' +
    '       b.[type] IN (''FN'',''IF'') ' +
    '   ) ' +
    '   OR ' +
    '   ( ' +
            CAST(@IncludeTriggers AS VARCHAR(1)) + ' = 1 ' +
    '       AND ' +
    '       b.[type] IN (''TR'') ' +
    '   ) ' +
    '); ';

IF @DebugMode = 0
BEGIN
    INSERT INTO @Results EXEC(@Query);
END;
ELSE
BEGIN
    PRINT 'Select Statement:  ' + @SelectStatement;
    PRINT 'Query:  ' + @Query;
END;

IF @DebugMode = 0
BEGIN
    SELECT 
        [ObjectType]
        ,[ObjectName]
        ,[ColumnName]
        ,[Value]
        ,[Count] = CASE
            WHEN [ObjectType] IN ('USER TABLE') THEN COUNT(1)
            ELSE NULL
        END
        ,[SelectStatement]
    FROM @Results
    GROUP BY [ObjectType], [ObjectName], [ColumnName], [Value], [SelectStatement]
    ORDER BY [Value];
END;

/********************** STRING_SPLIT() FUNCTION **********************    
CREATE FUNCTION STRING_SPLIT (
    @Expression nvarchar(4000)
    ,@Delimiter nvarchar(100)
)
RETURNS @Ret TABLE ([value] NVARCHAR(4000))
AS
BEGIN

    DECLARE @Start INT = 0, @End INT, @Length INT;
    SELECT @End = CHARINDEX(@Delimiter,@Expression), @Length = @End - @Start;

    IF @End <= 0
    BEGIN
        INSERT INTO @Ret ([value]) VALUES (@Expression);
    END
    ELSE
    BEGIN
        WHILE @Length >= 0
        BEGIN
            INSERT INTO @Ret ([value])
                SELECT ltrim(rtrim(substring(@Expression,@Start,@Length)));
    
            SELECT @Start = @End + LEN(@Delimiter)
            SELECT @End = CHARINDEX(@Delimiter,@Expression,@Start)
            IF @End < 1
                SELECT @End = LEN(@Expression) + 1;
            SELECT @Length = @End - @Start;
    
        END;
    END;
    RETURN;
END;

*********************************************************************/

```
