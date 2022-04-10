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
