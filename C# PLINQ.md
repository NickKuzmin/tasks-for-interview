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
