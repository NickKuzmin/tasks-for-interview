1. DB (ключи, индексы, связи…)
2. Entity Framework (жадная / ленивая загрузка)
3. С# .NET (DI, garbage collector…)
4. ASP.NET MVC (сессия, время сессии, где хранится…)

*C#:*

- https://metanit.com/sharp/interview/

- https://www.guru99.com/c-sharp-interview-questions.html

- https://www.c-sharpcorner.com/UploadFile/puranindia/C-Sharp-interview-questions/

- https://hackr.io/blog/c-sharp-interview-questions

- http://a4academics.com/interview-questions/52-dot-net-interview-questions/417-c-oops-interview-questions-and-answers

- https://www.softwaretestinghelp.com/c-sharp-interview-questions/

- https://tproger.ru/articles/problems/

- https://cmsmagazine.ru/journal/items-80-problems-with-it-interviews/

- https://habr.com/ru/post/351874/

- Отличия IEnumerable & IQueryable:
> https://habr.com/ru/post/256821/
> - Where<TSource>(this IEnumerable<TSource> source, Func<TSource, bool> predicate)
> - Where<TSource>(this IQueryable<TSource> source, Expression<Func<TSource, bool>> predicate)

*SQL:*

- https://habr.com/ru/company/otus/blog/461067/

- https://tproger.ru/articles/sql-interview-questions/

- https://proglib.io/p/sql-questions/

- https://techrocks.ru/2020/06/11/top-sql-interview-questions-1/

- https://jsehelper.blogspot.com/2016/01/sql-1.html

- https://vk.com/topic-51760813_34627260

- https://temofeev.ru/info/articles/luchshie-voprosy-sredney-slozhnosti-po-sql-na-sobesedovanii-analitika-dannykh/

- https://ru.bitdegree.org/rukovodstvo/sql-zadachi/

- http://sqlcom.ru/helpful-and-interesting/top-10-questions/

- https://oracle-patches.com/oracle/prof/341-tablichnaya-selektivnost-indeksnaya-selektivnost-blochnaya-selektivnost

- https://coderlessons.com/tutorials/bazy-dannykh/osnovy-subd/18-klasternyi-protiv-neklasterizovannogo-indeksa

*React.js:*
- https://proglib.io/p/react-digest/

*Unit-testing:*

- https://gist.github.com/vertigra/696e9d92dc72070584e556e2169e850d

- https://habr.com/ru/post/116372/

- https://www.maxshulga.ru/2012/03/mock-vs-stub.html
-----------------
*C#:*

- ReaderWriterLocker
- Monitor
- Mutex
- EventWaitHandler
- InterLocked
- IValidatableObject
- Records - тип
- Policy.Handle

*SQL:*
- ACID
- Нормальные формы
- MapReduce
- Типы индексов
- Оконные функции
- Транзакции
- Хранимые процедуры
- Триггеры
- Функции агрегаций
- Алгоритм "Векторых часов"
- Фильтр Блума
- Репликация данных
- Типы БД: Реляционные, хранилища ключей и значений (Memcached, Redis, Riak), столбцовые (ClickHouse, Cassandra, HBase), документные (MongoDB, CouchDB, RavenDB), графовые (Neo4J, Infinite Grapg)
- Уровни изоляции
- B-tree
- Теорема CAP
- Репликация (одноранговая, ведущий-ведомый)
- Согласованность, долговечность
- Кворумы записи
- Агрегаты
- Типы распределения данных: репликация, фрагментация
- Пессиместический и оптимистический подходы к обеспечению согласованности данных
- UAT/QA/DEV
- Многовариантная персистентность
- Порождающие события (event sourcing)
- DataMapper/Repository patterns
- HTTP - Stateless-протокол

*REST WEB API:*
- Swagger
- [FromBody][FromQuery] атрибуты
- HEAD/GET/POST/PUT/PATCH/DELETE
- HttpRepl (A command-line tool for interacting with RESTful HTTP services)
-----------------------------
Табличная селективность или селективность строк – соотношение количества строк, возвращаемых запросом к общему количеству строк в таблице.

Индексная селективность - отношение числа строк соответствующих конкретному ключевому значению к общему числу строк в индексе.
 
Селективность индекса – это показатель того, сколько строк от общего числа приходится на одно ключевое значение индекса.
Селективность хороша, если мало строк имеют одинаковые ключевые значения.

Характеристика кластерного индекса
Стандартное и отсортированное хранилище данных
Используйте только один или несколько столбцов для индекса
Помогает хранить данные и индексировать вместе
фрагментация
операции
Сканирование кластеризованного индекса и поиск индекса
Поиск ключей

Характеристики некластеризованных индексов
Хранить только значения ключей
Указатели на строки кучи / кластерного индекса
Позволяет вторичный доступ к данным
Мост к данным
Операции сканирования индекса и поиска индекса
Вы можете создать некластеризованный индекс для таблицы или представления
Каждая строка индекса в некластеризованном индексе хранит значение некластеризованного ключа и локатор строк.
--------------------------
Управление сеансами и состояниями в ASP.NET Core
Способ хранения данных	Механизм хранения
Файлы Cookie	Файлы cookie HTTP. Могут содержать данные, сохраненные с помощью кода приложения на стороне сервера.
Состояние сеанса	Файлы cookie HTTP и код приложения на стороне сервера
TempData	Файлы cookie HTTP или состояние сеанса
Строки запросов	Строки запросов HTTP
Скрытые поля	Поля формы HTTP
HttpContext.Items	Код приложения на стороне сервера
Кэш	Код приложения на стороне сервера
