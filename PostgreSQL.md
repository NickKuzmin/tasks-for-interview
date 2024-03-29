- `PgAdmin`
- `cd C:\Program Files\PostgreSQL\14\bin`
- `psql.exe -U postgres`
- `\l`
- `\c <databasename>`
- `\dt`
- `\dt *.*`
- `\dt public.*`
- `\dt dbo.*`
- `C:\Program Files\PostgreSQL\14\data\pg_hba.conf`
- Нейминг в нижнем регистре: 
```
[Table("person")]
public class Person
```
- EntityFramework:
```
<entityFramework>
    <providers>
      <provider invariantName="Npgsql" type="Npgsql.NpgsqlServices, Npgsql.EntityFramework" />
    </providers>
  </entityFramework>
  <system.data>
    <DbProviderFactories>
      <remove invariant="Npgsql"/>
      <add name="Npgsql Data Provider" invariant="Npgsql" description=".Net Data Provider for PostgreSQL" type="Npgsql.NpgsqlFactory, Npgsql, Culture=neutral, PublicKeyToken=5d8b90d52f46fda7" support="FF"/>
    </DbProviderFactories>
  </system.data>
  <connectionStrings>
    <add name="ArticleContext" connectionString="host=localhost;port=5432;database=entityframeworksamples;user id=postgres;password=<secretpassword>" providerName="Npgsql" />
  </connectionStrings>
```
---------------------------------------------- 
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
- upsert postgresql
- B-Tree индекс
- Index Seek vs Index Scan
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
**Приведение типов:**

```
CREATE OR REPLACE FUNCTION type_testing(money_val float8) RETURNS void AS $$
BEGIN
	RAISE NOTICE 'ran %', money_val
END;
$$ LANGUAGE plpgsql;

SELECT type_testing(0.5);
SELECT type_testing(0.5::float4);
SELECT type_testing(1);
```

```
CREATE OR REPLACE FUNCTION type_testing(money_val int) RETURNS void AS $$
BEGIN
	RAISE NOTICE 'ran %', money_val
END;
$$ LANGUAGE plpgsql;

SELECT type_testing(1);
SELECT type_testing(0.5::int);
SELECT type_testing(0.4::int);
SELECT type_testing(CAST(0.5 as int)));

--SELECT type_testing('1.5');
--SELECT type_testing('1.5'::int);
SELECT type_testing('1.5'::numeric::int);

SELECT 'abc' || 1;
SELECT ' 10 ' == 10;
```
----------------------------------------------
- `VACUUM FULL`
- `VACUUM ANALYZE`
----------------------------------------------
- `Индексное сканирование (Index scan)`
- `Исключительно ндексное сканирование (Index scan only)`
- `Сканирование по битовой карте (bitmap scan)`
- `Последовательное сканирование (sequential scan)`
----------------------------------------------
**Типы индексов:**
- `Balanced tree`: (Создается по умолчанию. Поддерживает операции '<, >, <=, >=, ='. Поддерживает LIKE. Индексирует NULL. Сложность: O(logn)):
```
CREATE INDEX <index_name> ON <table_name> (column_name))
```

- `Hash`: (O(1), только по сравнению '=')
```
CREATE INDEX <index_name> ON <table_name> USING HASH (column_name))
```

- `GiST (обобщенное дерево поиска)`
- `GIN (обобщенный обратный)`
- `SP-GiST (GiST с двоичным разбиением пространства)`
- `BRIN (блочный-диапазонный)`
----------------------------------------------
**Explain:**

```
EXPLAIN query
```

```
EXPLAIN ANALYZE query
```

```
ANALYZE [table_name[(column1, columne2, ...)]]
```
----------------------------------------------
**Индекс по выражению:**

```
CREATE INDEX idx_performance_test_annotation ON performance_test(annotation));

EXPLAIN
SELECT *
FROM performance_test
WHERE annotation LIKE 'AB%'
```

```
CREATE INDEX idx_performance_test_annotation ON performance_test(LOWER(annotation)));

EXPLAIN
SELECT *
FROM performance_test
WHERE LOWER(annotation) LIKE 'ab%'
```
----------------------------------------------
**Массивы:**

```
CREATE TABLE chess_game
(
	white_player text,
	black_player text,
	moves text[],
	final_state text[][]
);

INSERT INTO chess_game
VALUES ('Ivan', 'Andrew', '{ "d4", "d5", "c4", "c6" },
	'{{ "Ra8", "Qe8", "x", "x", "x" },
	{{ "a7", "A1", "x", "x", "x" },
	{{ "b5", "B4", "x", "x", "x", "x", "x", "x" }}');
	

INSERT INTO chess_game
VALUES ('Ivan', 'Andrew',
	ARRAY['d4', 'd5', 'x', 'x'],
	ARRAY[
		['d4', 'd5', 'x', 'x'],
		['d5', 'd5', 'x', 'x'],
		['d6', 'd5', 'x', 'x']
	]
);
```

```
SELECT moves[2:3]
FROM chess_game;

SELECT moves[:3]
FROM chess_game;

SELECT moves[2:]
FROM chess_game;
```

```
SELECT array_dims(final_state), array_dims(moves, 1)
FROM chess_game;
```

```
UPDATE chess_game
SET moves = ARRAY['d4', 'd5', 'x', 'x'];

UPDATE chess_game
SET moves[4] = 'g6';
```
----------------------------------------------
**Операторы массивов:**

```
SELECT ARRAY[1, 2, 3, 4] = ARRAY[1, 2, 3, 4]; -- true
SELECT ARRAY[1, 2, 4, 3] = ARRAY[1, 2, 3, 4]; -- false

SELECT ARRAY[1, 2, 4, 3] > ARRAY[1, 2, 3, 4]; -- true
SELECT ARRAY[1, 2, 4, 3] > ARRAY[1, 2, 5, 4]; -- false

SELECT ARRAY[1, 2, 4, 3] @> ARRAY[1, 2]; -- true
SELECT ARRAY[1, 2, 4, 3] @> ARRAY[1, 2, 5]; -- false

SELECT ARRAY[1, 2] @< ARRAY[1, 2, 5]; -- true
SELECT ARRAY[1, 2, 6] @< ARRAY[1, 2, 5]; -- false

SELECT ARRAY[1, 2, 3, 4] && ARRAY[1, 2]; -- true
SELECT ARRAY[1, 2, 3, 4] && ARRAY[5]; -- false
```
----------------------------------------------
**VARIADIC:**

```
CREATE FUNCTION filter_even(VARIADIC numbers int[]) RETURNS SETOF int AS $$
DECLARE
	counter int;
BEGIN
	FOREACH counter IN ARRAY numbers
	LOOP
		CONTINUE WITH counter % 2 != 0;
		RETURN NEXT counter;
	END LOOP;
END;
$$ LANGUAGE plpgsql;

SELECT * FROM filter_even(1, 2, 3, 4, 5, 6);
SELECT * FROM filter_even(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
```
----------------------------------------------
**Пользовательские типы:**

1) `Домен` - пользовательские типы данных с ограничениями.
2) `Составной тип` - тип, объединяющий логически взаимосвязанные данные без создания полноценной таблицы.
3) `Перечисления` - позволяет эмулировать простейшие справочные таблицы.
----------------------------------------------
**Пользовательские типы:**

```
CREATE DOMAIN text_no_space_null AS TEXT NOT NULL CHECK (value ~ '^(?!\s*$).+');

CREATE TABLE agent (
	first_name text_no_space_null,
	last_name text_no_space_null
);

INSERT INTO agent
VALUES ('bob', 'taylor);

ALTER DOMAIN text_no_space_null ADD CONSTRAINT text_no_space_null_length32 CHECK (LENGTH(value) <= 32) NOT VALID;

ALTER DOMAIN text_no_space_null VALIDATE CONSTRAINT text_no_space_null_length32;
```
----------------------------------------------
**Композитный тип:**

```
CREATE TYPE price_bounds AS (
	max_price real,
	min_price real
);

CREATE FUNCTION get_price_bounderies() RETURNS SETOF price_bounds AS $$
	SELECT MAX(unit_price), MIN(unit_price)
	FROM products
$$ LANGUAGE SQL;
```

```
CREATE TYPE complex AS (
	r float8,
	i float8
);

CREATE TABLE math_calcs (
	math_id serial,
	val complex
);

INSERT INTO math_calcs
VALUES
(ROW(3.0, 4.0)),
(ROW(3.0, 4.0));

SELECT * FROM math_calcs;

SELECT (val).* FROM math_calcs;
SELECT (math_calcs.val).r FROM math_calcs;

UPDATE math_calcs
SET val = ROW(5.0, 4.0);
```
----------------------------------------------
**Перечисления:**

```
CREATE TYPE game_type AS ENUM
('Football', 'Hockey', 'Box');

ALTER TYPE game_type
ADD VALUE 'Volleyball' AFTER 'Box';

CREATE TABLE game (
	id serial PRIMARY KEY,
	gametype game_type
);
```
----------------------------------------------
**ROLLUP/GROUPING/CUBE:**

```
SELECT supplier_id, category_id, SUM(units_in_stock)
FROM products
GROUP BY GROUPING SETS ((supplier_id), (supplier_id, category_id))
ORDER BY supplier_id, category_id NULLS FIRST;
```

```
SELECT supplier_id, SUM(units_in_stock)
FROM products
GROUP BY ROLLUP(supplier_id);
```

```
SELECT supplier_id, category_id, SUM(units_in_stock)
FROM products
GROUP BY ROLLUP (supplier_id, category_id)
ORDER BY supplier_id, category_id NULLS FIRST;
```

```
SELECT supplier_id, category_id, reorder_level, SUM(units_in_stock)
FROM products
GROUP BY ROLLUP (supplier_id, category_id, reorder_level)
ORDER BY supplier_id, category_id NULLS FIRST;
```

```
SELECT supplier_id, category_id, SUM(units_in_stock)
FROM products
GROUP BY CUBE (supplier_id, category_id)
ORDER BY supplier_id, category_id NULLS FIRST;
```
----------------------------------------------
**Команды PSQL:**

- `\c <dbname>` - переключиться на БД
- `\l` - список БД
- `\dn` - список схем
- `\dt` - все таблицы текущей БД
- `\d <tablename>` - описание таблицы
- `\dv` - все view-представления БД
- `\df` - все функции БД
- `\du` - все роли в экземпляре кластера
- `\g` - повторить предыдущую команду
- `\i <filename>` - выполнить команду из файла
- `\?` - список команд psql
- `\q` - выйти из psql
----------------------------------------------
**CSV:**

```
\copy databasename FROM 'C:\database.csv' DELIMITER ',' CSV HEADER;
```
----------------------------------------------
**CTE:**

```
WITH customer_countries AS
(
	SELECT country FROM customers
)
SELECT company_name
FROM suppliers
WHERE country IN (SELECT * FROM customer_countries)
```
----------------------------------------------
**Recursive CTE:**

```
WITH RECURSIVE submission(sub_line, employee_id) AS
(
	SELECT last_name, employee_id FROM employee WHERE manager_id IS NULL
	UNION ALL
	SELECT sub_line || ' -> ' || e.last_name, e.employee_id
	FROM employee, submission
	WHERE employee.manager_id = s.employee_id
)
SELECT * FROM submission;
```
----------------------------------------------
**Оконные функции:**

- **Оконные функции** - позволяют обрабатывать группу строк без образования группировок в результирующем наборе.
- Отрабатывают после JOIN, WHERE, GROUP BY, HAVING, но перед ORDER BY

- `ROW_NUMBER` - присвоение уникального значения строкам
- `RANK` - присвоение ранга (веса) строкам С пропусками
- `DENSE_RANK` - присвоение ранга (веса) строкам БЕЗ пропусками
- `LAG` - присвоение значения текущей строке, основанной на значении в предыдущей
- `LEAD` - НАОБОРОТ присвоение значения текущей строке, основанной на значении в следующей

- **Агрегатные функции:** `SUM`, `AVG`, `MIN`, `MAX`, `COUNT`
- **Ранжирование:** `ROW_NUMBER`, `RANK`, `LAG`, `LEAD`

```
SELECT category_id, AVG(unit_price) AS avg_price --, category_name
FROM products
GROUP BY category_id; --, category_name
```

```
SELECT category_id, category_name, product_name, unit_price, AVG(unit_price)
OVER (PARTITION BY category_id) AS avg_price,
FROM products
JOIN categories USING(category_id);
```

```
SELECT product_name, units_in_stock,
	RANK() OVER(ORDER BY product_id)
FROM products;
```

```
SELECT product_name, units_in_stock,
	RANK() OVER(ORDER BY units_in_stock)
FROM products;
```

```
SELECT product_name, units_in_stock,
	DENSE_RANK() OVER(ORDER BY units_in_stock)
FROM products;
```

```
SELECT product_name, units_in_stock,
	DENSE_RANK() OVER(
		ORDER BY
			CASE
				WHEN unit_price > 80 THEN 1
				WHEN unit_price > 30 AND unit_price < 80 THEN 2
				ELSE 3
			END
	)
	AS ranking
FROM products;
```

```
SELECT product_name, units_in_stock,
	LAG(unit_price) OVER(ORDER BY unit_price DESC) - unit_price AS price_lag
FROM products
ORDER BY unit_price DESC;
```

```
SELECT product_name, units_in_stock,
	LEAD(unit_price) OVER(ORDER BY unit_price DESC) - unit_price AS price_lag
FROM products
ORDER BY unit_price DESC;
```

```
SELECT *
FROM (SELECT product_id, product_name, category_id, unit_price, units_in_stock,
	ROW_NUMBER() OVER (ORDER BY unit_price DESC) AS nth
	FROM products
	) AS sorted_prices
WHERE nth < 4
ORDER BY unit_price;
```
----------------------------------------------
**Транзакции:**

- `READ UNCOMMITED`
- `READ COMMITED`
- `REPEATABLE READ`
- `SERIALIZABLE`

- В начале транзакций: `BEGIN ISOLATION LEVEL <level>`
- Внутри транзакции: `SET TRANSACTION ISOLATION LEVEL <level>`

```
BEGIN;

UPDATE employee SET Name = 'name';
DELETE FROM employee;

COMMIT;
```

```
BEGIN;

UPDATE employee SET Name = 'name';

SAVEPOINT backup;

DELETE FROM employee;

ROOLBACK TO backup;
```
----------------------------------------------
**Triggers:**

- **Построчные триггеры**
- **Триггеры на утверждение**

**Построчные триггеры:**
```
CREATE OR REPLACE FUNCTION track_changes_on_customers() RETURNS trigger AS $$
BEGIN
	NEW.last_updated = now();
	RETURN NEW;
END
$$ LANGUAGE plpgsql;

CREATE TRIGGER customers_timestamp BEFORE INSERT OR UPDATE ON customers
	FOR EACH ROW EXECUTE PROCEDURE track_changes_on_customers();
```

**Триггеры на утверждение:**
```
CREATE OR REPLACE FUNCTION build_audit_products() RETURNS trigger AS $$
BEGIN
	IF TG_OP = 'INSERT' THEN
		INSERT INTO products_audit
		SELECT 'I', session_user, now(), nt.* FROM new_table nt;
	ELSEIF TG_OP = 'UPDATE' THEN
		INSERT INTO products_audit
		SELECT 'U', session_user, now(), nt.* FROM new_table nt;
	ELSEIF TG_OP = 'DELETE' THEN
		INSERT INTO products_audit
		SELECT 'D', session_user, now(), nt.* FROM new_table nt;
	ENDIF;
	RETURN NULL;
END
$$ LANGUAGE plpgsql;

CREATE TRIGGER audit_products_insert AFTER INSERT ON customers
REFERENCING OLD TABLE AS old_table
FOR EACH STATEMENT EXECUTE PROCEDURE build_audit_products();

CREATE TRIGGER audit_products_update AFTER UPDATE ON customers
REFERENCING OLD TABLE AS old_table
FOR EACH STATEMENT EXECUTE PROCEDURE build_audit_products();

CREATE TRIGGER audit_products_delete AFTER DELETE ON customers
REFERENCING OLD TABLE AS old_table
FOR EACH STATEMENT EXECUTE PROCEDURE build_audit_products();
```
----------------------------------------------
**Roles:**

```
CREATE ROLE <rolename> LOGIN
```
	
```
CREATE USER <username>
```

```
CREATE ROLE sales_stuff;
CREATE USER john_smith WITH PASSWORD 'qwerty';
REVOKE CREATE ON SCHEMA public FROM public;
REVOKE ALL ON DATABASE northwind FROM public;
GRANT CONNECT ON DATABASE northwind TO sales_stuff;
GRANT USAGE ON SCHEMA public TO sales_stuff;
GRANT CREATE ON SCHEMA public TO sales_stuff;
GRANT USAGE ON DATABASE public TO sales_stuff;
GRANT sales_stuff TO john_smith;
```

```
SELECT grantee, privilege_type
FROM information_schema.role_table_grants
WHERE table_name = 'admin_demo2'
```
----------------------------------------------
**Права на уровне таблицы:**

```
SELECT grantee, privilege_type
FROM information_schema.role_table_grants
WHERE table_name = 'admin_demo2'
```

```
GRANT SELECT, INSERT, UPDATE, DELETE ON TABLE
public.orders,
public.order_details
TO sales_stuff;
GRANT SELECT ON TABLE public.employees to sales_stuff;

GRANT SELECT, INSERT, UPDATE, DELETE, REFERENCES, TRIGGER ON ALL TABLES
IN SCHEMA public
TO northwind_admins;
```

**Права на уровне колонок:**

```
GRANT SELECT (employee_id, last_name) ON employees TO sales_stuff;

REVOKE SELECT ON employees ON sales_stuff;
```

**Права на уровне строк:**

```
ALTER TABLE products
ENABLE ROW LEVEL SECURITY;

CREATE POLICY active_products_for_sales_stuff ON products
FOR SELECT
TO sales_stuff
USING (reorder_level > 10);
```

**Изъятие привилегий:**

```
REVOKE ALL PRIVILEGES ON employees, orders, order_details, products FROM sales_stuff;
REVOKE ALL ON DATABASE northwind FROM sales_stuff;
REVOKE ALL ON SCHEMA public FROM sales_stuff;
```

```
DROP ROLE sales_stuff;
DROP USER john_smith;
```
----------------------------------------------
**Партицирование таблиц:**

**Создание таблицы-партиции с использованием ключевого слова INHERITS:**
```
CREATE TABLE bigtable_y2021m03 (   
    CHECK (created_at >= '2021-03-01'::DATE AND created_at < '2021-04-01'::DATE) 
) INHERITS (bigtable);
								    
CREATE TABLE bigtable_y2021m04 (    
    CHECK (created_at >= '2021-04-01'::DATE AND created_at < '2021-05-01'::DATE)  
) INHERITS (bigtable);
```

**Добавление индексов, такие же, как в мастер-таблице:**
```
ALTER TABLE ONLY bigtable_y2021m03    
    ADD CONSTRAINT bigtable_y2021m03__pkey PRIMARY KEY (id);
								    
CREATE INDEX bigtable_y2021m03__created_at ON bigtable_y2021m03 (created_at);
								    
ALTER TABLE ONLY bigtable_y2021m04  
    ADD CONSTRAINT bigtable_y2021m04__pkey PRIMARY KEY (id);
								    
CREATE INDEX bigtable_y2021m04__created_at ON bigtable_y2021m04 (created_at);
```
								    
**Добавление индексов, такие же, как в мастер-таблице:**
```
CREATE OR REPLACE FUNCTION     
    bigtable_insert_trigger()
RETURNS TRIGGER AS $$
BEGIN
IF ( NEW.created_at >= '2021-03-01'::DATE AND 
    NEW.created_at < '2021-04-01'::DATE ) THEN    
        INSERT INTO bigtable_y2021m03 VALUES (NEW.*);
ELSIF ( NEW.created_at >= '2021-04-01'::DATE AND   
    NEW.created_at < '2021-05-01'::DATE ) THEN  
        INSERT INTO bigtable_y2021m04 VALUES (NEW.);
ELSE
    RAISE EXCEPTION 'Date out of range.   
        Fix the bigtable_insert_trigger() function!';
END IF;
RETURN NULL;
END;
$$
LANGUAGE plpgsql;							    
```

**Подключение функции к мастер-таблице:**
```
CREATE TRIGGER insert_bigtable    
    BEFORE INSERT ON bigtable
    FOR EACH ROW EXECUTE FUNCTION bigtable_insert_trigger();							    
```
			   
**Разнесение данных из мастер-таблицы по партициям:**
```
WITH x AS (  
    DELETE FROM ONLY bigtable      
        WHERE created_at BETWEEN .. AND .. RETURNING *)
INSERT INTO bigtable_y20XXmYY   
    SELECT * FROM x;							    
```
			   
**Очищение мастер-таблицы:**
```
TRUNCATE ONLY bigtable;					    
```
