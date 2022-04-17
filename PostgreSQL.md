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
---------------------------------------------- 
```
CREATE SEQUENCE seq1;

SELECT nextval('seq1');
SELECT currval('seq1');
SELECT lastval();

SELECT setval('seq1', 16, true);
```

```
CREATE SEQUENCE IF NOT EXISTS seq2 INCREMENT 16;
```

```
CREATE SEQUENCE IF NOT EXISTS seq3
INCREMENT 16
MINVALUE 0
MAXVALUE 128
START WITH 0;
```

```
CREATE TABLE book
(
	book_id INT NOT NULL
);

CREATE SEQUENCE IF NOT EXISTS book_book_id_seq
START WITH 1 OWNED 1 BY book.book_id;

ALTER TABLE book
ALTER COLUMN book_id SET DEFAULT nextval('book_book_id_seq');
```	
----------------------------------------------
**Запрет на самостоятельное указание идентификатора:**

```
CREATE Table book
(
	book_id int GENERATED ALWAYS AS IDENTITY NOT NULL
);

-- INSERT INTO book VALUES(1);
INSERT INTO book
OVERRIDING SYSTEM VALUE
VALUES(1);
```
----------------------------------------------
**RETURNING:**
```
INSERT INTO book (title)
VALUES ('Title #1')
RETURNING book_id;
```

```
INSERT INTO book (title)
VALUES ('Title #1')
RETURNING *;
```
----------------------------------------------
**Functions:**

```
CREATE OR REPLACE FUNCTION fix_customer_region() RETURNS void AS $$
	UPDATE tmp_customers
	SET region = 'unknown'
	WHERE region IS NULL
$$ LANGUAGE SQL;
```

```
SELECT fix_customer_region();
```
