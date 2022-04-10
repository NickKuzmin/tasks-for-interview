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
