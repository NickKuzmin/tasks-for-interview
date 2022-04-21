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
---------------------------------------------------------------
**AggregateException:**

```
int Square(int n) => n * n;

object[] numbers = new object[] { 1, 2, 3, 4, 5, "6" };
 
var squares = from n in numbers.AsParallel()
                 let x = (int)n
                 select Square(x);
try
{
    squares.ForAll(n => Console.WriteLine(n));
}
catch (AggregateException ex)
{
    foreach (var e in ex.InnerExceptions)
    {
        Console.WriteLine(e.Message);
    }
}
```
---------------------------------------------------------------
**WithCancellation:**

```
int Square(int n)
{
    var result = n * n;
    Console.WriteLine($"Квадрат числа {n} равен {result}");
    Thread.Sleep(1000); // имитация долгого вычисления
    return result;
}

CancellationTokenSource cts = new CancellationTokenSource();
new Task(() =>
{
    Thread.Sleep(400);
    cts.Cancel();
}).Start();
 
try
{
    int[] numbers = new int[] { 1, 2, 3, 4, 5, 6, 7, 8, };
 
    var squares = from n in numbers
		.AsParallel()
		.WithCancellation(cts.Token)
	select Square(n);
 
    foreach (var n in squares)
        Console.WriteLine(n);
}
catch (OperationCanceledException)
{
    Console.WriteLine("Операция была прервана");
}
catch (AggregateException ex)
{
    if (ex.InnerExceptions != null)
    {
        foreach (Exception e in ex.InnerExceptions)
            Console.WriteLine(e.Message);
    }
}
finally
{
    cts.Dispose();
}
```
