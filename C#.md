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
-------------------------
- *Класс Mutex (mutual exclusion — взаимное исключение или мьютекс)* является одним из классов в .NET Framework, позволяющих обеспечить синхронизацию среди множества процессов. Он очень похож на класс Monitor тем, что тоже допускает наличие только одного владельца. Только один поток может получить блокировку и иметь доступ к защищаемым мьютексом синхронизированным областям кода.
Мьютекс представляет собой взаимно исключающий синхронизирующий объект. Это означает, что он может быть получен потоком только по очереди. Мьютекс предназначен для тех ситуаций, в которых общий ресурс может быть одновременно использован только в одном потоке.

- *Семафор* - подобен мьютексу, за исключением того, что он предоставляет одновременный доступ к общему ресурсу не одному, а нескольким потокам. Поэтому семафор пригоден для синхронизации целого ряда ресурсов. Семафор управляет доступом к общему ресурсу, используя для этой цели счетчик. Если значение счетчика больше нуля, то доступ к ресурсу разрешен. А если это значение равно нулю, то доступ к ресурсу запрещен. С помощью счетчика ведется подсчет количества разрешений.
-------------------------
*Возможные проблемы при работе в многопоточной среде:*

- Deadlock — взаимная блокировка.
- Race-Condition — состояние гонки. Ситуация, в которой поведение и результат вычислений, выполняемых программой, зависит от работы планировщика потоков среды выполнения.
- Busy-Wait — проблема, при которой программа потребляет ресурсы процессора не для вычислений, а для ожидания.
- Thread-Starvation — проблема, при которой в программе слишком много одновременно работающих потоков.

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
 - С помощью оператора new в куче для хранения объекта CLR выделяет участок памяти. А в стек добавляет адрес на этот участок памяти.
 
- Так же надо отметить, что для крупных объектов существует своя куча - Large Object Heap. В эту кучу помещаются объекты, размер которых больше 85 000 байт. Особенность этой кучи состоит в том, что при сборке мусора сжатие памяти не проводится по причине больших издержек, связанных с размером объектов.

- Кроме того, чтобы снизить издержки от работы сборщика мусора, все объекты в куче разделяются по поколениям.
Всего существует три поколения объектов: 0, 1 и 2-е:

- К поколению 0 относятся новые объекты, которые еще ни разу не подвергались сборке мусора. К поколению 1 относятся объекты, которые пережили одну сборку, а к поколению 2 - объекты, прошедшие более одной сборки мусора.

- Когда сборщик мусора приступает к работе, он сначала анализирует объекты из поколению 0. Те объекты, которые остаются актуальными после очистки, повышаются до поколения 1.

- Если после обработки объектов поколения 0 все еще необходима дополнительная память, то сборщик мусора приступает к объектам из поколения 1. Те объекты, на которые уже нет ссылок, уничтожаются, а те, которые по-прежнему актуальны, повышаются до поколения 2.
-------------------------
- IDisposable - механизм для освобождения неуправляемых ресурсов
- CancellationToken - ...
- 
