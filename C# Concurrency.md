- Linq to Events (System.Reactive) - "Push"-model
- Linq to Object/Entities - "Pull"-model

- Реактивное программирование основано на концепции "наблюдаемых потоков". Подписавшись на поток - вы будете получать любое количество элементов данных (OnNext), поток может завершить на (OnError) или уведомление о завершении потока (OnCompleted).

```
interface IObserver<in T>
{
  void OnNext(T item);
  void OnCompleted();
  void OnError(Exception error);
}

interface IObservable<out T>
{
  IDisposable Subscribe(IObserver<TResult> observer);
}
```

```
Obserable.Interval(TimeSpan.FromSeconds(1))
  .Timestamp()
  .Where(x => x.Value % 2 == 0)
  .Select(x => x.Timestamp)
  .Subscribe(x => Trace.WriteLine(x),
    ex => Trace.WriteLine(ex));
```
-----------------------------------------------------------------------------------
- `Конкурентные коллекции` и `Неизменяемые коллекциию`
- `Чистая функция` - не имеет побочных эффектов.
- `System.Collections.Immutable`
-----------------------------------------------------------------------------------
```
Task<T> NotImplementedAsync<T>()
{
  return Task.FromException<T>(new NotImplemenetedException());
}
```
-----------------------------------------------------------------------------------
```
async Task MyMethodAsync(IProgress<double> progress)
{
  bool done = false;
  double percentComplete = 0;
  while (!done)
  {
    // ...
    progress?.Report(percentComplete);
  }
}

var progress = new Progress<double>();
progress.ProgressChanged += (sender, args) =>
{
  // ...
};
await MyMethodAsync(progress);
```
----------------------------------------------------------------------------------
```
Task task1 = Task.Delay(TimeSpan.FromSeconds(1));
Task task2 = Task.Delay(TimeSpan.FromSeconds(2));

await Task.WhenAll(task1, task2);
```

```
Task<int> task1 = Task.FromResult(3);
Task<int> task2 = Task.FromResult(5);

int[] results = await Task.WhenAll(task1, task2);
```

```
Task<int> task1 = client.GetResultAsync();
Task<int> task2 = client.GetResultAsync();

Task<int> completedTask = await Task.WhenAny(task1, task2);

int result = await completedTask;
```
