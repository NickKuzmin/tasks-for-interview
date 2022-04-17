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
----------------------------------------------
**Scalar functions:**

```
CREATE OR REPLACE FUNCTION get_total_number_of_goods() RETURNS bigint AS $$
	SELECT SUM(unit_price)
	FROM products
$$ LANGUAGE SQL;
```

```
SELECT get_total_number_of_goods();
```

```
CREATE OR REPLACE FUNCTION get_avg_price() RETURNS float8 AS $$
	SELECT AVG(unit_price)
	FROM products
$$ LANGUAGE SQL;
```

```
SELECT get_avg_price();
```
----------------------------------------------
- `IN` - входящие аргументы
- `OUT` - исходящие аргументы
- `INOUT` - и входящие, и исходящие аргументы
- `VARIADIC` - массив входящих параметров
- `DEFAULT` value

```
CREATE OR REPLACE FUNCTION get_product_by_name(prod_name varchar) RETURNS real AS $$
	SELECT unit_price
	FROM products
	WHERE product_name = prod_name
$$ LANGUAGE SQL;

SELECT get_product_by_name('Chocolate') as price;
```

```
CREATE OR REPLACE FUNCTION get_price_bounderies(OUT max_price real, OUT min_price real) RETURNS real AS $$
	SELECT MAX(unit_price), MIN(unit_price)
	FROM products
$$ LANGUAGE SQL;

SELECT get_price_bounderies();
SELECT * FROM get_price_bounderies();
```

```
CREATE OR REPLACE FUNCTION get_price_bounderies_by_discontinuity(IN fs_discontinued int, OUT max_price real, OUT min_price real) RETURNS real AS $$
	SELECT MAX(unit_price), MIN(unit_price)
	FROM products
	WHERE discontinued = fs_discontinued
$$ LANGUAGE SQL;

SELECT get_price_bounderies_by_discontinuity(100);
SELECT * FROM get_price_bounderies_by_discontinuity(100);
```

```
CREATE OR REPLACE FUNCTION get_price_bounderies_by_discontinuity(IN fs_discontinued int DEFAULT 1, OUT max_price real, OUT min_price real) RETURNS real AS $$
	SELECT MAX(unit_price), MIN(unit_price)
	FROM products
	WHERE discontinued = fs_discontinued
$$ LANGUAGE SQL;

SELECT get_price_bounderies_by_discontinuity();
SELECT * FROM get_price_bounderies_by_discontinuity();
```
----------------------------------------------
