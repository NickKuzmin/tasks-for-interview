**AsParallel:**
(параллельное, непоследовательные вычисления)
```
int Square(int n) => n * n;

int[] numbers = new int[] { 1, 2, 3, 4, 5, 6, 7, 8, };
var squares = from n in numbers.AsParallel()
         select Square(n);
 
foreach (var n in squares)
    Console.WriteLine(n);
```
---------------------------------------------------------------
**ForAll:**

```
int Square(int n) => n * n;
int[] numbers = new int[] { 1, 2, 3, 4, 5, 6, 7, 8, };
 
(from n in numbers.AsParallel() select Square(n)).ForAll(Console.WriteLine);
 
numbers.AsParallel().Select(n => Square(n)).ForAll(Console.WriteLine);
```
---------------------------------------------------------------
**AsOrdered/AsUnordered:**

```
int[] numbers = new int[] { -2, -1, 0, 1, 2, 3, 4, 5, 6, 7, 8, };
var squares = from n in numbers.AsParallel().AsOrdered()
              where n > 0
              select Square(n);
 
var query = from n in squares.AsUnordered()
            where n > 4
            select n;
 
foreach (var n in query)
    Console.WriteLine(n);
 
int Square(int n) => n * n;
```
