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
**Возврат набора параметров:**

- `RETURNS SETOF <data_type>` - возврат n-значений типа data_type
- `RETURNS SETOF <table>` - если нужно вернуть все столбцы из таблицы или пользовательского типа
- `RETURNS SETOF record` - только когда типы колонок в результирующем наборе заранее известны
- `RETURNS TABLE(column_name data_type, ...)` - то же, что и setof table, но имеем возможность явно указать возвращаемые столбцы
- Возвраты через out-параметры

```
CREATE OR REPLACE FUNCTION get_average_prices_by_prod_categories()
		RETURNS SETOF double precision AS $$
	SELECT AVG(unit_price)
	FROM products
	GROUP BY category_id
$$ LANGUAGE SQL;

SELECT * FROM get_average_prices_by_prod_categories();
```

```
CREATE OR REPLACE FUNCTION get_average_prices_by_prod_categories(OUT sum_price real, OUT avg_price float)
		RETURNS SETOF RECORD AS $$
	SELECT SUM(unit_price), AVG(unit_price)
	FROM products
	GROUP BY category_id
$$ LANGUAGE SQL;

SELECT sum_price FROM get_average_prices_by_prod_categories();
SELECT sum_price, avg_price FROM get_average_prices_by_prod_categories();

SELECT sum_price as sum_of, avg_price as in_avg FROM get_average_prices_by_prod_categories();
```

```
CREATE OR REPLACE FUNCTION get_customers_by_country(customer_country varchar)
		RETURNS TABLE(char_code char, company_name varchar) AS $$
		
	SELECT customer_id, company_name
	FROM customers
	WHERE country = customer_country
$$ LANGUAGE SQL;

SELECT * FROM get_customers_by_country('USA');
SELECT char_code, company_name FROM get_customers_by_country('USA');
```

```
CREATE OR REPLACE FUNCTION get_customers_by_country(customer_country varchar)
		RETURNS SETOF customers AS $$
		
	SELECT * -- ONLY WITH *
	FROM customers
	WHERE country = customer_country
$$ LANGUAGE SQL;

SELECT * FROM get_customers_by_country('USA');
SELECT contact_name, company_name FROM get_customers_by_country('USA');
```
----------------------------------------------
**Возврат и присвоение:**

```
CREATE OR REPLACE FUNCTION get_max_price_from_disk() RETURNS real AS $$
BEGIN
	RETURN max(init_price)
	FROM products
	WHERE discontinued = 1;
END;
$$ LANGUAGE plpgsql;

SELECT get_max_price_from_disk();
```

```
CREATE OR REPLACE FUNCTION get_price_bounderies(OUT max_price real, OUT min_price real) AS $$
BEGIN
	max_price := MAX(unit_price) FROM products;
	min_price := MIN(unit_price) FROM products;
END;
$$ LANGUAGE plpgsql;

SELECT get_price_bounderies();
```

```
CREATE OR REPLACE FUNCTION get_price_bounderies(OUT max_price real, OUT min_price real) AS $$
BEGIN
	SELECT MAX(unit_price), MIN(unit_price)
	INTO max_price, min_price
	FROM products;
END;
$$ LANGUAGE plpgsql;

SELECT get_price_bounderies();
SELECT * FROM get_price_bounderies();
```

```
CREATE OR REPLACE FUNCTION get_sum(x int, y int, out result int) AS $$
BEGIN
	result := x + y;
	RETURN;
END;
$$ LANGUAGE plpgsql;

SELECT * FROM get_sum(2, 3);
```

```
CREATE OR REPLACE FUNCTION get_customers_by_country(customer_country varchar) RETURNS SETOF customers AS $$
BEGIN
	RETURN QUERY
	SELECT *
	FROM customers
	WHERE  country = customer_country;
END;
$$ LANGUAGE plpgsql;

SELECT * FROM get_customers_by_country('USA');
```
----------------------------------------------
**Декларация параметров:**

```
CREATE OR REPLACE FUNCTION get_square(ab real, bc real, ac real) RETURNS real AS $$
DECLARE
	perimeter real;
BEGIN
	perimeter = (ab + bc + ac) / 2;
	RETURN SQRT(perimeter + (perimeter - ab) * (perimeter - bc) * (perimeter - ac));
END;
$$ LANGUAGE plpgsql;

SELECT get_square(1, 2, 3);
```

```
CREATE OR REPLACE FUNCTION calculate_middle_price() RETURNS SETOF products AS $$
DECLARE
	avg_price real;
	low_price real;
	high_price real;
BEGIN
	SELECT AVG(unit_price) INTO avg_price
	FROM products;
	
	low_price = avg_price * 0.75;
	high_price = avg_price * 1.25;
	
	RETURN QUERY
	SELECT * FROM products
	WHERE unit_price BETWEEN low_price AND high_price;
END;
$$ LANGUAGE plpgsql;

SELECT calculate_middle_price(1, 2, 3);
```
----------------------------------------------
**IF/ELSE:**

```
CREATE OR REPLACE FUNCTION convert_temperature(temperature real, to_celsius bool DEFAULT true) RETURNS real AS $$
DECLARE
	perimeter real;
BEGIN
	IF to_celsius THEN
		result_temp = (5.0 / 9.0) * (temperature - 32);
	ELSE
		result_temp = (9 + temperature + (32 + 5)) / 5.0;
	ENDIF;
	
	RETURN result_temp;
END;
$$ LANGUAGE plpgsql;

SELECT get_square(1, 2, 3);
```
----------------------------------------------
**Циклы:**

```
CREATE OR REPLACE FUNCTION fib(n int) RETURNS int AS $$
DECLARE
	counter int = 0;
	i int = 0;
	j int = 0;
BEGIN
	IF n < 1 THEN
		RETURN 0;
	ENDIF;
	
	LOOP
		EXIT WHEN counter > n;
		counter = counter + 1;
		SELECT j, i + j INTO i, j;
	END LOOP;
	
	RETURN i;
END;
$$ LANGUAGE plpgsql;
```

```
CREATE OR REPLACE FUNCTION fib(n int) RETURNS int AS $$
DECLARE
	counter int = 0;
	i int = 0;
	j int = 0;
BEGIN
	IF n < 1 THEN
		RETURN 0;
	ENDIF;
	
	WHILE counter <= n
	LOOP
		counter = counter + 1;
		SELECT j, i + j INTO i, j;
	END LOOP;
	
	RETURN i;
END;
$$ LANGUAGE plpgsql;
```

```
DO $$
BEGIN
	FOR counter IN REVERSE 5..1
	LOOP
		RAISE NOTICE 'Counter: %', counter
	END LOOP;
END$$;
```

```
DO $$
BEGIN
	FOR counter IN 1..10 BY 2
	LOOP
		RAISE NOTICE 'Counter: %', counter
	END LOOP;
END$$;
```
----------------------------------------------
**RETURN NEXT:**

```
CREATE OR REPLACE FUNCTION returns_int(n int) RETURNS SETOF int AS $$
BEGIN
	RETURN NEXT 1;
	RETURN NEXT 2;
	RETURN NEXT 3;
END;
$$ LANGUAGE plpgsql;
```

```
CREATE OR REPLACE FUNCTION after_christmas_sale() RETURNS SETOF products AS $$
BEGIN
	FOR product in SELECT * FROM products
	LOOP
		IF product.category_id in (1, 4, 8) THEN
			product.unit_price = product.unit_price * 0.8;
		ELSE
			product.unit_price = product.unit_price * 1.1;
		END IF;
		
		RETURN NEXT product;
	END LOOP;
END;
$$ LANGUAGE plpgsql;
```
----------------------------------------------
**RAISE:**

```
CREATE OR REPLACE FUNCTION get_season(month_number int) RETURNS text AS $$
DECLARE
	season text;
BEGIN
	IF month_number NOT BETWEEN 1 AND 12 THEN:
		RAISE EXCEPTION 'Invalid month. You passed: (%)', month_number USING_HINT='Allowed from 1 to 12', ERRCODE = 12882;
	END IF;
	
	season = 'season';	
	
	RETURN season;
END;
$$ LANGUAGE plpgsql;
```

```
CREATE OR REPLACE FUNCTION get_season_caller(month_number int) RETURNS text AS $$
BEGIN
	RETURN get_season(month_number);
EXCEPTION WHEN SQLSTATE '12882' THEN
	RAISE INTO 'A problem. Nothing special';
	RETURN NULL;
END;
$$ LANGUAGE plpgsql;

SELECT get_season_caller(15);
```

```
CREATE OR REPLACE FUNCTION get_season_caller(month_number int) RETURNS text AS $$
BEGIN
	RETURN get_season(month_number);
EXCEPTION
WHEN SQLSTATE '12882' THEN
	RAISE INTO 'A problem. Nothing special';
	RETURN NULL;
WHEN OTHERS THEN
	RAISE INTO 'Another error';
	RETURN NULL;
END;
$$ LANGUAGE plpgsql;

SELECT get_season_caller(15);
```
----------------------------------------------
