```
of(1,2,3).pipe(
  map(value => value * 2)
).subscribe({
  next: console.log
});
```

```
of(1, 2, 3).pipe(
  // пропускаем только нечетные значения
  filter(value => value % 2 !== 0),
  map(value = value * 2)
).subscribe({
  next: console.log
});
```

```
const observable = new Observable((observer) => {
  observer.next(1);
  observer.next(2);
  observer.complete();
});
```
