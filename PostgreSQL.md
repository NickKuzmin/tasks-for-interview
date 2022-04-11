- SQL - Any MSSQL/Postgres
- SQL - ALL
- Trancate vs DELETE vs DROP
- Trancate Restart Identity
- Postgres: serial type
- Unique NOT NULL vs Primary Key (Unique - можно использовать для нескольких колонок таблицы)
- Unique NULL vs Unique NOT NULL
- Postgres: schema information (constraints and etc)
- FK syntax
- Check constraint
- Unique constraint
- Default constraint
- Postgres: sequences
- Postgres: Как работает serial под копотом?
---------------------------------------------- 
```
DROP TABLE IF EXISTS books;
```

```
SELECT *
FROM Book
WHERE Id > 10
LIMIT 20
```

```
SELECT book.Title || ' ' || book.Id
FROM book
```

```
SELECT *
FROM orders JOIN products USING(order_id) -- ON orders.order_id = employees.order_id
JOIN customers USING(order_id) -- ON orders.order_id = employees.order_id
JOIN employees USING(order_id) -- ON orders.order_id = employees.order_id
```

```
SELECT *
FROM orders
NATURAL JOIN employees
```
