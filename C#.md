*Synchronization primitives:*
- https://docs.microsoft.com/ru-ru/dotnet/standard/threading/overview-of-synchronization-primitives
- https://github.com/vit-h/SynchronizationPrimitives
- https://habr.com/ru/post/459514/
- Thread Synchronization in C# .Net made easy! | Lock | Monitor | Mutex | Semaphore: https://www.youtube.com/watch?v=5Zv8fF-KPrE

*Below are the list of Primitives:*

- AutoResetEvent
- ManualResetEvent
- ManualResetEventSlim
- Semaphore
- SemaphoreSlim
- Mutex
- Monitor
- Lock
- CountdownEvent
- Barrier
- Interlocked
- Volatile
- ReaderWriterLock
- ReaderWriterLockSlim
- Concurrent Collections (ConcurrentQueue, ConcurrentStack, ConcurrentDictionary, ConcurrentBag)
- 
-------------------------
В этой же версии .NET Framework появился мини-framework для кооперативной отмены асинхронных операций. Состоит он из всего трёх типов:

- CancellationTokenSource — создаёт маркёры отмены (свойство Token) и обрабатывает запросы на отмену операции (перегруженные методы Cancel/CancelAfter).
- CancellationToken — маркёр отмены; позволяет несколькими способами отслеживать запросы на отмену операции: опросом свойства IsCancellationRequested, регистрацией callback-функции (через перегруженный метод Register), ожиданием на объекте синхронизации (свойство WaitHandle).
- OperationCanceledException — исключение, выброс которого по соглашению означает, что запрос на отмену операции был обработан и операция должна считаться отменённой. Предпочтительный способ генерации исключения — вызов метода CancellationToken. ThrowIfCancellationRequested.

-------------------------
*Asynchronous vs Multithreading and Multiprocessing Programming:*
- Asynchronous vs Multithreading and Multiprocessing Programming: https://www.youtube.com/watch?v=0vFgKr5bjWI
- Distinguish Asynchronous And Multi-Threading: https://www.youtube.com/watch?v=Kfs84d7jaT8
-------------------------
*Parallelism vs Concurrency:*
- https://tproger.ru/explain/concurrency-vs-parallelism/
- https://habr.com/ru/company/piter/blog/274569/
-------------------------
*NetCore:*
- IServiceProvider, Startup.ConfigureService
- DI: AddTransient/AddScoped/AddSingleton
-------------------------
```
HTTP Message Handlers in ASP.NET Web API:
```
https://docs.microsoft.com/en-us/aspnet/web-api/overview/advanced/http-message-handlers

https://habr.com/ru/post/424873/

-------------------------
*Polly Library:* https://github.com/App-vNext/Polly
- Retry
- Circuit-breaker
- Timeout
- Bulkhead Isolation
- Cache
- Fallback
- PolicyWrap


-------------------------
- IDisposable - механизм для освобождения неуправляемых ресурсов
- CancellationToken - ...
- 
