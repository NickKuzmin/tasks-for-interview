-------------------------
**К ссылочным типам относятся:**

- class
- interface
- delegate
- object
- string

**Значимые типы:**
- Структуры (struct)
- Перечисления (enum)
-------------------------
**Жизненный цикл сервиса определяют следующие три метода:**

- **AddTransient**
Transient подразумевает, что сервис создается каждый раз, когда его запрашивают. Этот жизненный цикл лучше всего подходит для легковесных, не фиксирующих состояние, сервисов.

- **AddScoped**
Scoped - сервис создаются единожды для каждого запроса.

- **AddSingleton**
Singleton - сервис создается при первом запросе (или при запуске ConfigureServices, если вы указываете инстанс там), а затем каждый последующий запрос будет использовать этот же инстанс.
-------------------------
- Рекомендации Microsoft по выбору class/struct: https://docs.microsoft.com/ru-ru/dotnet/standard/design-guidelines/choosing-between-class-and-struct
1) Выделение и освобождение типов значений являются общими дешевле, чем выделение и освобождение ссылочных типов.
2) Типы значений упаковываются при приведении к ссылочному типу или к одному из интерфейсов, которые они реализуют. Они будут распакованы при приведении обратно к типу значения. Так как поля представляют собой объекты, выделенные в куче и собираемые сборщиком мусора, слишком много упаковки и распаковки могут негативно повлиять на кучу, сборщик мусора и в конечном итоге производительность приложения. В отличие от этого, такая упаковка не происходит, так как ссылочные типы являются приведенными
3) Присваивания больших ссылочных типов дешевле, чем присваивания типов больших значений.
4) Изменения в экземпляр ссылочного типа влияют на все ссылки, указывающие на экземпляр. Экземпляры типа значения копируются, когда они передаются по значению. При изменении экземпляра типа значения это само по себе не влияет на его копии. Поскольку копии не создаются явным образом пользователем, но неявно создаются при передаче аргументов или возвращении возвращаемых значений, типы значений, которые могут быть изменены, могут вызвать путаницу для многих пользователей. Поэтому типы значений должны быть неизменяемыми.
-------------------------
- Управляемая память в .Net поделена на стек и несколько хипов. Самые важные из хипов – это обычная (эфемерная) куча и LOH. Эфемерная куча – это то место, где живут все обычные объекты. LOH – это то место где живут большие (больше 85000 байт) объекты.
- LOH обладает некоторыми особенностями:
1) Объекты в LOH никогда не перемещаются
2) LOH только растет и никогда не уменьшается (т.е. если объект собран сборщиком мусора, размер LOH все равно остается неизменным)
3) Хип LOH освобождается только тогда, когда LOH полностью пуст
-------------------------
**Monitor vs Lock:**
- Monitor is no different from lock but the monitor class provides more control over the synchronization of various threads trying to access the same lock of code.

```
Monitor.Enter 
Monitor.TryEnter
Monitor.Exit
Monitor.Wait
Monitor.Pulse
Monitor.PulseAll
```
-------------------------
- **SemaphoreSlim** - это упрощенная альтернатива Semaphore, которую можно использовать для синхронизации в рамках одного процесса. SemaphoreSlim Класс представляет упрощенный, быстрый семафор, который можно использовать для ожидания внутри одного процесса, когда предполагается, что времена ожидания будут очень короткими.
- **ReaderWriterLockSlim** 
- **ManualResetEventSlim** - этот класс можно использовать для лучшей производительности, чем ManualResetEvent когда ожидается очень короткое время ожидания и когда событие не пересекает границу процесса.

- One difference is that SemaphoreSlim does not permit named semaphores, which can be system-wide. This would mean that a SemaphoreSlim could not be used for cross-process synchronization.
- The SemaphoreSlim class represents a lightweight, fast semaphore that can be used for waiting within a single process when wait times are expected to be very short.
- ReaderWriterLockSlim is similar to ReaderWriterLock, but it has simplified rules for recursion and for upgrading and downgrading lock state. ReaderWriterLockSlim avoids many cases of potential deadlock. In addition, the performance of ReaderWriterLockSlim is significantly better than ReaderWriterLock. ReaderWriterLockSlim is recommended for all new development.
- ReaderWriterLockSlim is not thread-abort safe. You should not use it in an environment where threads accessing it can be aborted, such as .NET Framework. If you're using .NET Core or .NET 5+, it should be fine. Abort is not supported in .NET Core and is obsolete in .NET 5 and later versions.
-------------------------
- Lookup vs Dictionary
-------------------------
```
IEnumerable — единственное что нужно это пройти по всем элементам коллекции. Read-only доступ к коллекции
ICollection — возможность изменять коллекцию и узнать ее размер
IList — возможность изменение коллекции. В дополнении становится доступен порядок (индекс элементов)

public interface IEnumerable
{
    IEnumerator GetEnumerator();
}

public interface IEnumerable<out T> : IEnumerable
{
    IEnumerator<T> GetEnumerator();
}

public interface ICollection : IEnumerable
{
    int Count { get; }  
    bool IsSynchronized { get; }
    Object SyncRoot { get; }
 
    void CopyTo(Array array, int index);
}

public interface ICollection<T> : IEnumerable<T>, IEnumerable
{
    int Count { get; }
    bool IsReadOnly { get; }
 
    void Add(T item);
    void Clear();
    bool Contains(T item);
    void CopyTo(T[] array, int arrayIndex);
    bool Remove(T item);
}

public interface IList : ICollection, IEnumerable
{
    bool IsFixedSize { get; }
    bool IsReadOnly { get; }
    Object this[int index] { get; set; }
 
    int Add(Object value);
    void Clear();
    bool Contains(Object value);
    int IndexOf(Object value);
    void Insert(int index, Object value);
    void Remove(Object value);
    void RemoveAt(int index);
}

public interface IList<T> : ICollection<T>, IEnumerable<T>, IEnumerable
{
    T this[int index] { get; set; }
 
    int IndexOf(T item);
    void Insert(int index, T item);
    void RemoveAt(int index);
}
```
-------------------------
```
[AttributeUsage(AttributeTargets.Class)]
public class SomeNewAttribute : System.Attribute
{
// ...
}
```

```
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Struct)]
AttributeTargets:
- All: используется всеми типами
- Assembly: атрибут применяется к сборке
- Constructor: атрибут применяется к конструктору
- Delegate: атрибут применяется к делегату
- Enum: применяется к перечислению
- Event: атрибут применяется к событию
- Field: применяется к полю типа
- Interface: атрибут применяется к интерфейсу
- Method: применяется к методу
- Property: применяется к свойству
- Struct: применяется к структуре
```
-------------------------
- При запуске приложения операционная система создает для него отдельный *процесс, которому выделяется определённое адресное пространство в памяти и который изолирован от других процессов*. *Процесс может иметь несколько потоков*. Как минимум, процесс содержит один - главный поток. В приложении на C# точкой входа в программу является метод Main. Вызов этого метода автоматически создает главный поток. А из главного потока могут запускаться вторичные потоки.
-------------------------

- Thread Class should be used when you need the ability to cancel your asynchronous operation. [General Definition: Threading enables your C# program to perform concurrent processing so you can do more than one operation at a time.]

- Thread Pool Class should be used when you need to schedule asynchronous operation and do not need return value or/and ability to cancel your operation [General Definition: A thread pool is a collection of threads that can be used to perform several tasks in the background. This leaves the primary thread free to perform other tasks asynchronously.]

- Delegates (using BeginInvoke/EndInvoke) should be used when you need to achieve some return value from your asynchronous operation. [General Definition: A delegate is a type that references a method. Once a delegate is assigned a method, it behaves exactly like that method. The delegate method can be used like any other method, with parameters and a return value.]

```
Thread MyNewThread = new Thread (MyFunction); 
MyNewThread.Start();
```

```
System.Threading.ThreadPool.QueueUserWorkItem(new System.Threading.WaitCallback(SomeLongTask)); 
System.Threading.ThreadPool.QueueUserWorkItem(new System.Threading.WaitCallback(AnotherLongTask));
```

```
Task.Factory.StartNew(CheckPrimeNumber);
Task.Factory.StartNew(CheckParameterPrimeNumber, 1000000021);

Task task = Task.Factory.StartNew(CheckParameterPrimeNumber, 1000000021);
while (!task.IsCompleted)
{ continue; }

Action dlgt = CheckPrimeNumber;
Task.Factory.FromAsync(dlgt.BeginInvoke, GetDividerFinished, null);

Task task = new Task(GetCompressedDataFromWebService);
task.ContinueWith(UncompressData).ContinueWith(UseUncompressedData);
task.Start();

Task<long> task = Task.Factory.StartNew<long>(GetDivider, 1000000021);
var result = task.Result;

CancellationTokenSource ctSource = new CancellationTokenSource();
CancellationToken token = ctSource.Token; 
var task = Task.Factory.StartNew<long>(() => GetDivider(1000000021, token), token);
ctSource.Cancel();

Parallel.For((long)(1000000021 - 20), (long)(1000000021 + 20), CheckParameterPrimeNumber);
```
-------------------------
- Thread vs task vs background worker vs thread pool
- Monitor vs Lock
```
If you want more control to implement advanced multithreading solutions using TryEnter() Wait(), Pulse(), and PulseAll() methods, then the Monitor class is your option.
C# Monitor.wait(): A thread wait for other threads to notify.
Monitor.pulse(): A thread notify to another thread.
Monitor.pulseAll(): A thread notifies all other threads within a process
```
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
- Semaphore - задающий начальное количество входов и максимальное количество одновременных входов. Ограничивает число потоков, которые могут одновременно обращаться к ресурсу или пулу ресурсов.
- SemaphoreSlim - Представляет упрощенную альтернативу семафору Semaphore, ограничивающему количество потоков, которые могут параллельно обращаться к ресурсу или пулу ресурсов. SemaphoreSlim - также поддерживает использование токенов отмены, но не поддерживает именованные семафоры или использование дескриптора ожидания для синхронизации. The SemaphoreSlim class represents a lightweight, fast semaphore that can be used for waiting within a single process when wait times are expected to be very short.
- Mutex - Основную работу по синхронизации выполняют методы WaitOne() и ReleaseMutex(). Метод mutexObj.WaitOne() приостанавливает выполнение потока до тех пор, пока не будет получен мьютекс mutexObj. После выполнения всех действий, когда мьютекс больше не нужен, поток освобождает его с помощью метода mutexObj.ReleaseMutex(). Таким образом, когда выполнение дойдет до вызова mutexObj.WaitOne(), поток будет ожидать, пока не освободится мьютекс. И после его получения продолжит выполнять свою работу. В отличие от Monitor, класс Mutex может использоваться для межпроцессной синхронизации. Для этого нужно использовать именованный мьютекс, который виден в операционной системе. 
- Monitor
- Lock - сокращенная версия Monitor. 
- CountdownEvent
- Barrier
- Interlocked
- Volatile
- ReaderWriterLock - Определяет блокировку, которая поддерживает один пишущий поток и несколько читающих. ReaderWriterLock предоставляет отдельные методы для блокировки на чтение и на запись – AcquireReaderLock и AcquireWriterLock. Оба метода принимают аргумент-таймаут и генерируют исключение ApplicationException, если этот таймаут истекает (вместо возвращения false, как это делают остальные аналогичные методы, связанные с потоками). Таймаут может быть легко превышен, если ресурс пользуется популярностью. Блокировка снимается при помощи методов ReleaseReaderLock или ReleaseWriterLock. Эти методы поддерживают вложенные блокировки. Предоставляется также метод ReleaseLock, снимающий все вложенные блокировки за один вызов. (Далее можно вызвать RestoreLock для восстановления состояния всех блокировок, предшествовавшего вызову ReleaseLock – в подражание поведению Monitor.Wait).
- ReaderWriterLockSlim
- Структура System.Threading.SpinLock, как и Monitor, предоставляет монопольный доступ к общему ресурсу на основе доступности блокировки. Когда SpinLock пытается получить блокировку, которая недоступна, этот примитив будет ожидать в цикле, постоянно проверяя возможность получения блокировки.
- Concurrent Collections (ConcurrentQueue, ConcurrentStack, ConcurrentDictionary, ConcurrentBag)
-------------------------
- *Класс Mutex (mutual exclusion — взаимное исключение или мьютекс)* является одним из классов в .NET Framework, позволяющих обеспечить синхронизацию среди множества процессов. Он очень похож на класс Monitor тем, что тоже допускает наличие только одного владельца. Только один поток может получить блокировку и иметь доступ к защищаемым мьютексом синхронизированным областям кода.
Мьютекс представляет собой взаимно исключающий синхронизирующий объект. Это означает, что он может быть получен потоком только по очереди. Мьютекс предназначен для тех ситуаций, в которых общий ресурс может быть одновременно использован только в одном потоке.

- *Семафор* - подобен мьютексу, за исключением того, что он предоставляет одновременный доступ к общему ресурсу не одному, а нескольким потокам. Поэтому семафор пригоден для синхронизации целого ряда ресурсов. Семафор управляет доступом к общему ресурсу, используя для этой цели счетчик. Если значение счетчика больше нуля, то доступ к ресурсу разрешен. А если это значение равно нулю, то доступ к ресурсу запрещен. С помощью счетчика ведется подсчет количества разрешений.

- *Класс Monitor* - обладает одним важным преимуществом по сравнению с оператором lock в C#: он позволяет добавлять значение тайм-аута для ожидания получения блокировки. Таким образом, вместо того, чтобы ожидать блокировку до бесконечности, можно вызвать метод TryEnter и передать в нем значение тайм-аута, указывающее, сколько максимум времени должно ожидаться получение блокировки.
Monitor - позволяет синхронизировать доступ к области кода, вызывая и освобождая блокировку конкретного объекта путем вызова Monitor.Enter Monitor.TryEnter методов, и Monitor.Exit . Блокировки объектов предоставляют возможность ограничить доступ к блоку кода, обычно называемому критическим разделом. Пока поток владеет блокировкой объекта, другой поток не может получить эту блокировку.

- *Атрибут [Synchronization]* - атрибут уровня класса эффективно блокирует весь код членов экземпляра объекта, обеспечивая безопасность в отношении потоков.
-------------------------
```
private static object _locker = new object();

lock (_locker)
{ ... }
```

```
public class LockDemo
{
    private static object _locker = new object();
    private static bool _hasLock = false;
 
    public void UseLock()
    {
        lock (_locker)
        {
            Console.WriteLine("Lock");
        }
    }
 
    public void UseMonitor()
    {
        try
        {
            Monitor.Enter(_locker, ref _hasLock);
 
            Console.WriteLine("Monitor");
        }
        finally
        {
            Monitor.Exit(_locker);
            _hasLock = false;
        }
    }
}
```

```
try
{
    locker.AcquireReaderLock(Timeout.Infinite);
    if (m_Cache.ContainsKey(key))
        Console.WriteLine( "For key {0} reader value is {1}.", key, m_Cache[key]);
}
finally
{
    locker.ReleaseReaderLock();
}

try
{
    locker.AcquireWriterLock(Timeout.Infinite);

    if (m_Cache.ContainsKey(key))
        Console.WriteLine("For key {0} reader value is {1}.", key, m_Cache[key]);
    else
    {
        m_Cache[key] = key * key;
        Console.WriteLine("For key {0} written value is {1}.", key, m_Cache[key]);
    }
}
finally
{
    locker.ReleaseWriterLock();
}

```
-------------------------
*Возможные проблемы при работе в многопоточной среде:*

- Deadlock — взаимная блокировка.
- Race-Condition — состояние гонки. Ситуация, в которой поведение и результат вычислений, выполняемых программой, зависит от работы планировщика потоков среды выполнения.
- Busy-Wait — проблема, при которой программа потребляет ресурсы процессора не для вычислений, а для ожидания.
- Thread-Starvation — проблема, при которой в программе слишком много одновременно работающих потоков.

-------------------------
**Concurrent collections:**
- ConcurrentQueue<T>
- ConcurrentStack<T>
- ConcurrentBag<T>
- ConcurrentDictionary<TKey, TValue>
- BlockingCollection<T>
------------------------
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

- **Поколение 0.** Идентифицируется новый только что размещённый объект, который ещё никогда не помечался как надлежащий удалению в процессе сборки мусора. Это самое молодое поколение содержит короткоживущие объекты. Примером короткоживущего объекта является временная переменная. Сборка мусора чаще всего выполняется в этом поколении.

- **Поколение 1.** Идентифицирует объект, который уже «пережил» один процесс сборки мусора (был помечен, как надлежащий удалению, но не был удалён из-за достаточного свободного места в куче). Это поколение содержит коротко живущие объекты и служит буфером между короткоживущими и долгоживущими объектами.

- **Поколение 2.** Идентифицирует объект, который пережил более одного прогона сбора мусора. Это поколение содержит коротко живущие объекты и служит буфером между короткоживущими и долгоживущими объектами.
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

------------------------
**Lazy:**

```
class Test
{
    private readonly Lazy<Blob> _lazy = new Lazy<Blob>();

    public Blob BlobData
    {
        get
        {
            return _lazy.Value;
        }
    }
}

Или:

private Lazy<Blob> _lazy = new Lazy<Blob>(() => new Blob());

Или:
class Test
{
    private Blob _blob;
    public Blob BlobData => LazyInitializer.EnsureInitialized(ref _blob);
}
```
------------------------
**Asymptotic complexity of .NET collection classes:**
**Type of Search/Collection Types**           *8Complexity**  **Comments**
Linear search Array/ArrayList/LinkedList  **O(N)**        Unsorted data.
Binary search sorted Array/ArrayList/     **O(log N)**    Requires sorted data.
Search Hashtable/Dictionary<T>            **O(1)**        Uses hash function.
Binary search SortedDictionary/SortedKey  **O(log N)**    Sorting is automated.

**Retrieval and Insertion:**

Operation         Array/ArrayList  LinkedList  SortedDictionary  SortedList
Access back       O(1)             O(1)        O(log N)          O(log N)
Access front      O(1)             O(1)        N.A.              N.A.
Access middle     O(1)             O(N)        N.A.              N.A.
Insert at back    O(1)             O(1)        O(log N)          O(N)
Insert at front   O(N)             O(1)        N.A.              N.A.
Insert in middle  O(N)             O(1)        N.A.              N.A.
------------------------
**Интерфейс может включать в себя:**
- Методы
- Свойства
- Индексаторы
- События
- Статические поля и константы (начиная с версии C# 8.0)
------------------------
- **Куча больших объектов (Large Object Heap, LOH)** - это специальная область, зарезервированная для размещения очень больших объектов. Большими считаются объекты, занимающие больше 85 Кбайт памяти. Это - пороговое значение относится к одному объекту, а не к графу объектов с корнем в данном объекте, поэтому массив из 1000 строк (по 100 символов в каждой) не считается большим объектом, так как сам массив содержит лишь 4- или 8-байтные ссылки на строки, а вот массив из 50 000 целых чисел - это большой объект.
------------------------
**Структуры:**
- Value type => при присвоении (передачи в метод) все поля и свойства копируются, не может быть null
- Нет наследования
- Поддерживает интерфейсы
- Если есть конструктор, в нем должны устанавливаться все поля и свойства
------------------------
- Expression Tree - ...
------------------------
- **Динамическая загрузка сборок** - ...
- **Позднее связывание** - ...    
------------------------
- Asp .Net Identity - ...
- Asp .Net Membership - ...    
------------------------  
- Task<TResult> vs ValueTask<TResult>
------------------------ 
 - Реализация с помощью лямбда-выражений
С помощью лямбд можно сократить определение замыкания:
```
var outerFn = () =>
{
    int x = 10;
    var innerFn = () => Console.WriteLine(++x);
    return innerFn;
};
 
var fn = outerFn();   // fn = innerFn, так как outerFn возвращает innerFn
// вызываем innerFn
fn();   // 11
fn();   // 12
fn();   // 13
```
------------------------
- **Event (Событие)** - это особый тип делегата, который облегчает событийно-ориентированное программирование. События — это члены класса, которые нельзя вызывать вне класса независимо от спецификатора доступа. Так, например, событие, объявленное как public, позволило бы другим классам использовать += и -= для этого события, но запуск события (то есть вызов делегата) разрешен только в классе, содержащем событие. Даже если событие объявлено как public, оно не может быть запущено напрямую нигде, кроме как в классе, в котором оно находится. Используя ключевое слово event, компилятор защищает наше поле от нежелательного доступа.
    
------------------------   
- Differences Between .NET Framework, .NET Core, and .NET Standard: https://code-maze.com/differences-between-net-framework-net-core-and-net-standard/    
- https://gosha20777.github.io/code/2018/02/22/dotnetcore/    
- Алгоритмическая сложность коллекций: https://docs.microsoft.com/ru-ru/dotnet/standard/collections/    
- Runtime Complexity of .NET Generic Collection: http://c-sharp-snippets.blogspot.com/2010/03/runtime-complexity-of-net-generic.html
