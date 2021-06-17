Типы констрейнтов:

Check constraint
Default constraint
Foreign key
Primary key
Unique clustered index
Unique constraint
Unique index

https://dataedo.com/kb/query/sql-server/list-all-table-constraints
--------------------------------------------
> select * from INFORMATION_SCHEMA.COLUMNS 
> where COLUMN_NAME like '%COLUMN_NAME%' 
> order by TABLE_NAME
--------------------------------------------
> SELECT *
> FROM INFORMATION_SCHEMA.TABLES 
> WHERE INFORMATION_SCHEMA.TABLES.TABLE_NAME like '%TABLE_NAME%'
--------------------------------------------
> SELECT sys.schemas.name AS T2,
>     t.NAME AS TableName,
>     p.rows AS RowCounts
> FROM 
>     sys.tables t
> INNER JOIN 
>     sys.partitions p ON t.object_id = p.OBJECT_ID 
> JOIN sys.schemas ON t.schema_id = sys.schemas.schema_id
> WHERE 
>     t.NAME LIKE '%TABLE_NAME%' 
>     AND t.is_ms_shipped = 0
>     AND p.rows <> 0
> GROUP BY 
>     t.Name, sys.schemas.name, p.Rows
> ORDER BY 
>     t.Name
--------------------------------------------
> SELECT  K.TABLE_NAME ,
>     K.COLUMN_NAME ,
>     K.CONSTRAINT_NAME
> FROM    INFORMATION_SCHEMA.TABLE_CONSTRAINTS AS C
>         JOIN INFORMATION_SCHEMA.KEY_COLUMN_USAGE AS K ON C.TABLE_NAME = K.TABLE_NAME
>                                                          AND C.CONSTRAINT_CATALOG = K.CONSTRAINT_CATALOG
>                                                          AND C.CONSTRAINT_SCHEMA = K.CONSTRAINT_SCHEMA
>                                                          AND C.CONSTRAINT_NAME = K.CONSTRAINT_NAME
> WHERE   C.CONSTRAINT_TYPE = 'PRIMARY KEY'
>         AND K.COLUMN_NAME = 'COLUMN_NAME';
--------------------------------------------
> DECLARE @xmltmp xml = (SELECT * FROM table FOR XML AUTO)
> PRINT CONVERT(NVARCHAR(MAX), @xmltmp)
