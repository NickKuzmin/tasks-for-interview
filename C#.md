-------------------------
- При запуске приложения операционная система создает для него отдельный *процесс, которому выделяется определённое адресное пространство в памяти и который изолирован от других процессов*. *Процесс может иметь несколько потоков*. Как минимум, процесс содержит один - главный поток. В приложении на C# точкой входа в программу является метод Main. Вызов этого метода автоматически создает главный поток. А из главного потока могут запускаться вторичные потоки.
-------------------------
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

- *Класс Monitor* - обладает одним важным преимуществом по сравнению с оператором lock в C#: он позволяет добавлять значение тайм-аута для ожидания получения блокировки. Таким образом, вместо того, чтобы ожидать блокировку до бесконечности, можно вызвать метод TryEnter и передать в нем значение тайм-аута, указывающее, сколько максимум времени должно ожидаться получение блокировки.
Monitor - позволяет синхронизировать доступ к области кода, вызывая и освобождая блокировку конкретного объекта путем вызова Monitor.Enter Monitor.TryEnter методов, и Monitor.Exit . Блокировки объектов предоставляют возможность ограничить доступ к блоку кода, обычно называемому критическим разделом. Пока поток владеет блокировкой объекта, другой поток не может получить эту блокировку.

- *Атрибут [Synchronization]* - атрибут уровня класса эффективно блокирует весь код членов экземпляра объекта, обеспечивая безопасность в отношении потоков.
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

- Поколение 0. Идентифицируется новый только что размещённый объект, который ещё никогда не помечался как надлежащий удалению в процессе сборки мусора

- Поколение 1. Идентифицирует объект, который уже «пережил» один процесс сборки мусора (был помечен, как надлежащий удалению, но не был удалён из-за достаточного свободного места в куче).

- Поколение 2. Идентифицирует объект, который пережил более одного прогона сбора мусора
-------------------------
- IDisposable - механизм для освобождения неуправляемых ресурсов
- CancellationToken - ...
- 
-------------------------
```
private static long GetDivider(long checkNumber){…}

private delegate void CheckPrimeNumberDelegate(long checkNumber);

CheckPrimeNumberDelegate dlgt = new CheckPrimeNumberDelegate(CheckPrimeNumber);
dlgt.BeginInvoke(1000000021, null, null);
```

```
private static long GetDivider(long checkNumber){…}

Thread trd = new Thread(new ThreadStart(CheckPrimeNumber));
trd.Start();
```

```
Thread trd = new Thread(new ParameterizedThreadStart(CheckParameterPrimeNumber));
trd.Start(1000000021);
```
