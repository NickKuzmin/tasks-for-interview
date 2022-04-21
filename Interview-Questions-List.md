**Полезные ресурсы для подготовки Ozon:**
- https://docs.microsoft.com/ru-ru/dotnet/standard/threading
- https://docs.microsoft.com/ru-ru/dotnet/csharp/programming-guide/concepts/async
- https://microservices.io/patterns/microservices.html
- https://www.postgresql.org/docs/13/index.html
- Вернон Вон «Предметно-ориентированное проектирование. Самое основное»
- Нархид Ния, Гвен Шапира «Apache Kafka. Потоковая обработка и анализ данных»
- Джеффри Рихтер «CLR via C#»
- Ганс-Юрген Шениг «PostgreSQL 11. Мастерство разработки»
- Задачи на ресурсе https://leetcode.com уровня easy и middle
--------------------------------------------
*Common:*
- https://github.com/senthil338/Software-Engineer-Interview

*Algorithms:*
- https://www.guru99.com/algorithm-interview-questions.html
- https://www.geeksforgeeks.org/top-10-algorithms-in-interview-questions/
- https://www.toptal.com/algorithms/interview-questions

*C#:*
- https://bool.dev/blog/detail/voprosy-na-sobesedovanii-po-c
- https://habr.com/ru/post/541194/
- https://metanit.com/sharp/interview/
- https://ivinsky.livejournal.com/3266.html
- https://itvdn.com/ru/blog/article/150-questions-net-developer
- https://devinterview.io/dev/cSharp-interview-questions
- https://ankitsharmablogs.com/csharp-coding-questions-for-technical-interviews/
- ASP .NET: https://www.wisdomjobs.com/e-university/asp-dot-net-interview-questions.html

*JavaScript:*
- https://chm.org.ua/javascript-interview/
- https://habr.com/ru/post/486820/
- https://github.com/lydiahallie/javascript-questions/tree/master/ru-RU
- https://github.com/sudheerj/javascript-interview-questions
- https://github.com/learning-zone/javascript-interview-questions

*React:*
- https://github.com/sudheerj/reactjs-interview-questions
- ReactJS: https://www.wisdomjobs.com/e-university/reactjs-interview-questions.html
- React 50 вопросов: https://t.me/js_by_vladilen/95

*Angular:*
- Angular: https://www.wisdomjobs.com/e-university/angular-4-interview-questions.html

*Database:*
- https://www.wisdomjobs.com/e-university/database-interview-questions.html
- MongoDB: https://www.wisdomjobs.com/e-university/mongodb-interview-questions.html
- PL/SQL: https://www.wisdomjobs.com/e-university/pl-sql-interview-questions.html

*HTML:*
- https://www.wisdomjobs.com/e-university/html-5-interview-questions.html

*CSS:*
- https://github.com/learning-zone/css-interview-questions
- https://www.wisdomjobs.com/e-university/bootstrap-4-interview-questions.html
- https://github.com/h5bp/Front-end-Developer-Interview-Questions

*DevOPS:*
- https://www.wisdomjobs.com/e-university/devops-interview-questions-answers.html

*GIT:*
- https://www.wisdomjobs.com/e-university/github-interview-questions.html

*Linux:*
- https://www.wisdomjobs.com/e-university/linux-interview-questions.html

*XML/WSDL/JSON/XPATH:*
- XPATH: https://www.wisdomjobs.com/e-university/xpath-interview-questions.html
- WSDL: https://www.wisdomjobs.com/e-university/wsdl-interview-questions.html
- XML: https://www.wisdomjobs.com/e-university/xml-interview-questions.html

*Cloud:*
- Azure: https://www.wisdomjobs.com/e-university/azure-b2c-interview-questions.html
- AWS: https://www.wisdomjobs.com/e-university/amazon-web-services-aws-interview-questions-answers.html

*LEETCODE:*
- https://github.com/jiajionline/LeetcodeSolutionWithMultipleLanguages
- 
----------------------------
- Azure Functions
- Реальный пример SOLID
- События и делегаты. Возможен ли вызов снаружи.
- Antiforgery tokens.
- GetHashCode/Equals.
- Чем функции от процедур отличаются.
- Как хранятся reference/value-типы
----------------------------
1. Dictionary<TKey, TValue> - что делать, если TKey планируется как составной ключ таблицы
2. Когда происходит перестроение страницы таблицы с кластерным индексом. Почему не сразу идет перестроение при вставке?
3.  Expression tree в связке с ORM
4. NO LOCK sql
5. Full/Simple backup
6. MediatR/CQRS
7. Статический конструктор статического класса
8. EF Transaction
9. Middleware
10. Оконные функции в SQL
11. CTE
12. REST, Идемпотентность, отсутствие Идемпотентности у POST
----------------------------
1. Может ли быть ссылочный тип в стеке (возможно, слишком очевидный вопрос, но я подзадумался - может есть какой-то специфичный случай, помимо того, что в стеке просто хранится ссылка на объект в куче) - stackalloc: https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/stackalloc
2. const - когда происходит инициализация (const declares a value that is determined at compile time. In the compiled code, it appears simply as a literal, rather than a reference to some named identifier. Constants are not initialised at all, they are constant values that are substituted at compile time.)
3. Как работает state machine для async/await
4. 200/300/400/500 - классификация кодов
5. Брокеры сообщений - каким принципам должны соответствовать
6. Распределенные транзакции
----------------------------
1) nginx/apache - как реализовать балансировку
2) cookie - клиент-серверное взаимодействие
3) zabix
4) Service Fabric
----------------------------
1) Контекст синхронизации
2) Slim версии синхронизации - чем отличается
3) Пример однопоточной асинхронной работы
4) ConfigureAwait в C#
5) async void vs async Task
6) ICollection vs IEnumerable
7) Рекомендации Microsoft по использованию Struct/Class
8) Finalizator vs IDisposable
9) Почему нельзя подиспоузить строку
10) z-index, position, display
11)  как изначально подойти к разработке разметки, чтобы не было хаотичного вставления Z-9000 -
12) VDOM vs DOM
----------------------------
Озон:
1) Roslyn vs Reflection
2) Event consistency/Event-driven programming 
3) CAP
4) async void, exception
5) await lock/Monitor/Mutex vs await Semaphore
6) uint
7) QuickSort
8) async/await - StateMachine
9) Задача - передан отсортированный целочисленный массив. Вернуть - массив квадратов элементов массива за линейное время
10) Стоит ли наследовать структуру от IDisposable?
----------------------------
1) Паттерн Repository/UnitOfWork
2) Обходы деревьев
3) Что может содержать интерфейс
----------------------------
1) CI vs CD
----------------------------
1) Бинарное дерево vs B-tree в контексте MSSQL
2) C# Select - детали реализации LINQ, yield
3) List vs Array
4) async task 150/100/50 - сколько будет потоков выделено, сколько суммарно займет времени. Вариант использования без async/await
5) Bad Practice Singleton, какие принципы нарушаются в SOLID
6) Singleton life-cycle. Нужен ли интерфейс, как подтягиваются зависимости, как работает в DI - singleton
7)
```
var i =0;
list = [1, 3, 5, 7, 9]

var result = list.Where(x => x > 3).Select(x => i++);
Console.WriteLine(i);

var item = result.First()
Console.WriteLine(item, i);
```
8)
```
select count(1), sum(1) from departments

select MAX(Uid) from Employee
select MAX(Salary) from Employee
```
----------------------------
1) Конструктор без параметров. Вызов конструктора без параметра внутри конструктора с параметра.
2) SQL: Batch, BulkCopy
3) AsNoTracking, DisableChangeTracking
4) lock(2) - lock от value типов
5) SPA
6) Как отключить рестарт IIS pool
----------------------------
1) Grasp
2) Луковая архитектура
3) Merge vs Rebase
4) Tslint, Solar Cube
5) Интерфейсы по умолчанию в C#
6) Новые фичи C#
7) LOH
8) IMemoryCache NetCore
9) NetCore BackgroundService
10) CORS
11) FIFO RabbitMQ
----------------------------
1) struct наследование. Почему невозможно.
2) Как происходит процесс боксинга
3) A и B имеют ссылку друг на друга и больше никто. Будут ли удалены из кучи
4) Типы куч. Когда чистится LOH
5) Финализатор, деструктор
6) Что могут содержать интерфейсы
7) Задача "AABBBC" -> "A2B3C"
8) Что переключает потоки
9) 4 потока или 2 потока на одной и тоже машине. Идет ли рост по скорости выполнения. Какие рекомендации по количеству потоков
10) Имеется ли у потока свой стек
11) Пессимистические и оптимистические блокировки
12) Типы блокировок. Типы классификации примитивов синхронизации
13) Interlock
14) Какое доступно количество потоков, как соотносится с RAM, количеством процессоров и тд
15) ValueTask
----------------------------
1) HashSet - конструктор с передачей компоратора, для сравнения ключей без учета регистра
2) ConfigureAwait, TaskScheduler
3) Await методы с WPF. Смена потока при выполнении таски
4) Навигационные проперти EF, Include
5) AsNotTracking
6) Некластерный индекс - как организована структура 
7) Сложность поиска по индексу
8) DbContext относительно жизненного цикла Singleton/Scoped/Transient?
9) Middleware vs HttpFilter
10) Валидация MVC
11) 400 vs 500. 503, отличия. Почему 500-ые не всегда необработанные ошибки
12) Политики доставки сообщения месседж брокеров
13) InMemory тесты
14) Dependency Injection vs Dependency Inversion. Что значит стрелка инверсии в этом принципе
15) MS Enqueue/ServiceBus
----------------------------
1) Records - ссылочный тип. Отличия от структур. Что такое
2) Casting: int -> long
long -> int
(object)long -> int
(object)int -> long
Где хранится, когда как object
3) ref - для значимых типов и ссылочных типов
4) ref для автопроперти
5) Возможен ли перевод из 0-го поколения сразу во 2-ое
6) Как работает финализатор
7) object - какие методы имеет. Как соотносится с ссылочными\значимыми типами
8) GetHashCode vs Equals - можно ли переопределять по отдельности? ЧТо будет если не переопределить что-то
9) Статический класс. Особенности
10) Статический конструкто
11) const vs readonly
12) UTF, Unicode
13) Интернирование строк. Синтаксис
14) delegate - стек или куча
15) Иммутабельные строки c#
16) Action vs Func
17) Как работает delegate под капотом
18) Подписанные сборки. Плюсы и минусы
19) IEnumerable vs IQueryable
20) Как запустить, отменить Task
21) Ковариантность-контрвариантность. IEnumerable/IList - что к чему относится и почему
22) Нормальные формы
24) Примеры реализации ACID принципов
25) Unique vs PK
----------------------------
**СМП:**

- JWT (синтаксис, видиы токенов, как использовать)
- Open API (Swagger) - описание контрактов yaml, генерация API
- Protobuf
- gRPC
- fanout vs topic vs другие типы в RabbitMQ
- Redis - сколько можно создать баз
- EF Core vs EF
- Database First/Code First/Model First (EDMX)
- Key, ForeignKey attributes
- FluentAPI EF
- Hangfire - режим работы, стратегии повторного запуска
- SelectMany для случая пустой коллекции в проперти
- async void - зачем нужен
- Aggregation exception - в каких случая. В контексте асинхронного кода
- configureAwait - синхронизация потоков
- Task vs ThreadPool vs Thread
- Parallel LINQ (PLINQ)
- Moq (loose-режим)
----------------------------
**C#:**
- Finalize vs Dispose
- Task vs Thread
- Event vs Delegate
- System.Array.CopyTo() vs System.Array.Clone()
- Throw ex vs Throw
----------------------------
- знание react: жизненный цикл, компоненты высшего порядка, хуки, redux-saga, знать и понимать общие архитектурные принципы - flux, mvvm
- знакомство с функциональным подходом: чистые функции, сайд эффекты, иммутабельность
- typescript: вспомогательные типы, type guards
----------------------------
- Cloud vs Web-hosting
----------------------------
- Как работает браузер
- Что такое DNS
- Как летят запросы
- Как работает handshake
- Для чего нужен CDN
- Как парсится респонс в браузере
- Что такое DHCP
- Как подгрузить стили асинхронно
- Как css и дом вместе соединяются
- Что такое requestAnimationFrame
- Этапы рендеринга в браузере
- Микро/макро/requestAnimationFrame - в чём разница
- Хэш таблица, скорость работы
- Map/Set/array в js
- Как написать факториал без циклов
- Хвостовая рекурсия(сами решили пообсуждать)
- mobx/redux
- webpack, babel, typescript
- Собиралки проектов gulp, webpack, ещё какие-то
- Прототипное наследование
- Селекторы css - приоритет
- Bubbling/drilling эвентов в дом
- В чём разница между обьектом и Map в js
- Когда выполняется requestAnimationFrame - до или после setTimout
- Анимация - какие свойства лучше анимировать
- Где быстрее анимация - на css или в js как-то
- Анимация - какие свойства лучше анимировать
- Где быстрее анимация - на css или в js
