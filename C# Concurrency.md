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
