- The overview of Database Paradigms:
https://tudip.com/blog-post/7-database-paradigms/
https://www.jigsawacademy.com/blogs/cloud-computing/database-sharding
--------------------------------------------
- mssql exection plan
--------------------------------------------
*Типы констрейнтов:*

- Check constraint
- Default constraint
- Foreign key
- Primary key
- Unique clustered index
- Unique constraint
- Unique index

- https://dataedo.com/kb/query/sql-server/list-all-table-constraints
--------------------------------------------
> select * from INFORMATION_SCHEMA.COLUMNS 
> where COLUMN_NAME like '%COLUMN_NAME%' 
> order by TABLE_NAME
--------------------------------------------
```
SELECT *
FROM INFORMATION_SCHEMA.TABLES 
WHERE INFORMATION_SCHEMA.TABLES.TABLE_NAME like '%TABLE_NAME%'
```
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
```
SELECT  K.TABLE_NAME,
K.COLUMN_NAME ,
K.CONSTRAINT_NAME
FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS AS C
JOIN INFORMATION_SCHEMA.KEY_COLUMN_USAGE AS K ON C.TABLE_NAME = K.TABLE_NAME
AND C.CONSTRAINT_CATALOG = K.CONSTRAINT_CATALOG
AND C.CONSTRAINT_SCHEMA = K.CONSTRAINT_SCHEMA
AND C.CONSTRAINT_NAME = K.CONSTRAINT_NAME
WHERE C.CONSTRAINT_TYPE = 'PRIMARY KEY'
AND K.COLUMN_NAME = 'COLUMN_NAME';
```
--------------------------------------------
```
DECLARE @xmltmp xml = (SELECT * FROM table FOR XML AUTO)
PRINT CONVERT(NVARCHAR(MAX), @xmltmp)
```
--------------------------------------------
```
CREATE TABLE A (
ID INT IDENTITY(1,1) PRIMARY KEY,
... Other Columns
)

CREATE TABLE B
(
ID UNIQUEIDENTIFIER DEFAULT NEWID() PRIMARY KEY,
... Other Columns
)

CREATE TABLE C
(
ID UNIQUEIDENTIFIER DEFAULT NEWSEQUENTIALID() PRIMARY KEY,
... Other Columns
)
```
--------------------------------------------
- How to Create Login, User & Assign Permissions in SQL Server: https://www.guru99.com/sql-server-create-user.html
--------------------------------------------
- Индексы создаются для столбцов таблиц и представлений. Индексы предоставляют путь для быстрого поиска данных на основе значений в этих столбцах. Например, если вы создадите индекс по первичному ключу, а затем будете искать строку с данными, используя значения первичного ключа, то SQL Server сначала найдет значение индекса, а затем использует индекс для быстрого нахождения всей строки с данными. Без индекса будет выполнен полный просмотр (сканирование) всех строк таблицы, что может оказать значительное влияние на производительность.
- Вы можете создать индекс на большинстве столбцов таблицы или представления. Исключением, преимущественно, являются столбцы с типами данных для хранения больших объектов (LOB), таких как image, text или varchar(max). Вы также можете создать индексы на столбцах, предназначенных для хранения данных в формате XML, но эти индексы устроены немного иначе, чем стандартные и их рассмотрение выходит за рамки данной статьи.
- Индекс состоит из набора страниц, узлов индекса, которые организованы в виде древовидной структуры — сбалансированного дерева. 
- Кластеризованный индекс хранит реальные строки данных в листьях индекса. Возвращаясь к предыдущему примеру, это означает что строка данных, связанная со значение ключа, равного 123 будет храниться в самом индексе. Важной характеристикой кластеризованного индекса является то, что все значения отсортированы в определенном порядке либо возрастания, либо убывания. Таким образом, таблица или представление может иметь только один кластеризованный индекс.
- Таблица не имеющая кластеризованного индекса называется кучей.
