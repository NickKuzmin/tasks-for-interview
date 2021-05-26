*C#:*

- ReaderWriterLocker
- Monitor
- Mutex
- EventWaitHandler
- InterLocked
- IValidatableObject
- Records - тип
- Policy.Handle
- TPL (Task Parallel Library)
- PLINQ (Parallel LINQ)
- Отличия IEnumerable & IQueryable (https://habr.com/ru/post/256821/):
  Where<TSource>(this IEnumerable<TSource> source, Func<TSource, bool> predicate)
  Where<TSource>(this IQueryable<TSource> source, Expression<Func<TSource, bool>> predicate)
- С# .NET (DI, garbage collector…)
- ASP.NET MVC (сессия, время сессии, где хранится…)
- Entity Framework (жадная / ленивая загрузка)  

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
- DB (ключи, индексы, связи…)

*HTTP/SOAP/REST:*
- X-Powered-By заголовок

*JavaScript frameworks and etc:*
- cypress
- Redux (dev-tools)
- Ember
- Backbone.js
- webpack
- React Native
- Babel
- VueJS
- Meteor
- Svelte
- Parcel (parceljs.org)
- Yarn 
- Jest
- Apollo
- Dart

*JavaScript:*
- EcmaScript https://github.com/lukehoban/es6features
- Prototype
- Контекст this, bind, call, apply
- Object.create (property descriptor). getters, setters
- Proxy
- Замыкание
- Стрелочные функции
- Promise/then/catch/finally/Promise.all/Promise.race
- async/await
- Event Loop (http://latentflip.com/)
- Взаимодействие с DOM
- Virtual DOM
- Методы массивов
- Деструктуризация
- Fetch, XMLHttpRequest (XHR), Ajax
- Генераторы-yield (Symbol iterator [Symbol.iterator], for of)
- Методы массивов (forEach, map, filter, reduce, find, findIndex)
- Map, Set, WeakMap, WeakSet
- Object.entries/Object.fromEntries
- Spread, Rest
- Деструктуризация для массивов и объектов
- LocalStorage (отличия LocalStorage от Cookies)
- var/let/const/Hoisting/const для array и объектов
- Возведение в степень **
- Глобальный объект global и window
- Параметры со значением по умолчанию (a = 10)
- startWith/endsWith/include/repeat/trim/padStart/padEnd
- Object.keys(this), Object.is, Object.assign, Object.entries, Object.values
- Описание полей объекта в [cityField + Date()]
- export модулей/import
- Статические методы
- Класс Symbol
- Reflect.construct/Reflect.apply/Reflect.ownKeys/Reflect.preventExtensions/Reflect.isExtensible
- `__proto__`
- V8 – в Chrome и Opera/SpiderMonkey – в Firefox

*JavaScript Unit-Testing:*
- Jasmine
- Ava
- Tape
- Mocha
- Jest
- React Testing Library (https://github.com/testing-library/react-testing-library)
- enzyme

*TypeScript:*
- ts.config (exclude, include, files, compiler options, target, source map, removeComments, noEmitOnError, noUnusedLocals, noUnusedParameters)
https://www.typescriptlang.org/docs/handbook/compiler-options.html
- Generic Types
function Sample<T extends object, R extends object>) : T & R
function Sample<T extends object, R extends keyof T>) : T & R
function Sample<T extends {new(..args)}>) : T & R
- Partial<T>
- entity as T
- Readonly<Array<string>>
- Декораторы
- Namespaces
- https://github.com/typestack/class-validator
- https://github.com/bcherny/programming-typescript-answers
- Code Style Conventions: https://github.com/akahan/typescript-style-guide

*NodeJS:*
- package.lock
- path/fs/os/events/http
- nodemon
- package-lock
- Gulp — это таск-менеджер для автоматического выполнения часто используемых задач (например, минификации, тестирования, объединения файлов)
- npx

*Backend Javascript:*
- NodeJS (Express, Nest, Koa, Loopback)
- Deno

*React.js:*
- Библиотека Prop-types
- UseContext / UseEffect

*Redux:*
- Не привязана к React.
- Component/Action/Store/Reducer
- dispatch/subscribe/getState
- combineReducers
- Middleware: Redux Thunk
- Redux logger
- Redux DevTools (Chrome)

*SSR:*
- Next.js (React)
- Nuxt.js (Vue)
- Angular Universal
- Sapper (Svelte)

*Serverless:*
- Firebase
- AWS
- JAMstack
- Yandex Cloud

*CSS:*
- CSS Grid
- Селекторы
- Box model
- Позиционирование
- FlexBox
- Псевдоэлементы
- Медиа запросы
- Препроцессоры (LESS/SASS)
- Bootstrap / Materialize CSS
- BEM

*Package manager:*
- npm
- yarn
  
*Performance:*
- yslow (http://yslow.org/)
- PageSpeed Insights (https://developers.google.com/speed/pagespeed/insights/)
- Chrome Dev Tools Device View
- Chrome Dev Tools Network Tab 
- Chrome Dev Tools Performance Tab (with screenshots and memery usage)
- gulp-imagemin
- imageoptim
- icomoon
- picturefill

*REST WEB API:*
- Swagger
- [FromBody][FromQuery] атрибуты
- HEAD/GET/POST/PUT/PATCH/DELETE
- HttpRepl (A command-line tool for interacting with RESTful HTTP services)

*Тестирование:*
- End 2 end
  
*Design Patterns & Code Style:*
- DDD
- TDD

*Other:*
- Progressive Web App
- FramerX/Figma
-----------------------------
*Git repositories:*

- Jest Unit-testing:
  https://github.com/leveluptuts/Level-Up-JavaScript-Testing-101

-----------------------------
*Youtube:*
- LevelUpTuts (https://www.youtube.com/channel/UCyU5wkjgQYGRB0hIHMwm2Sg)
- ITVDN (https://www.youtube.com/channel/UCzxRv9BtqrM946JmaMLtv_w)
- dotNET (https://www.youtube.com/channel/UCvtT19MZW8dq5Wwfu6B0oxw)
- Traversy Media (https://www.youtube.com/channel/UC29ju8bIPH5as8OGnQzwJyA)
- DotNext (https://www.youtube.com/channel/UCNPwMPudMEw-gnAT4zh_UZg)
- Hitesh Choudhary (https://www.youtube.com/channel/UCXgGY0wkgOzynnHvSEVmE3A)
- Hussein Nasser (https://www.youtube.com/c/HusseinNasser-software-engineering/)
- CODELLIGENT (https://www.youtube.com/channel/UC1sbu30ylZNM7ITdVxFF2ww)
- .NET Interview Preparation videos (https://www.youtube.com/c/dnfvideo/featured)
- DWDocumentary (https://www.youtube.com/c/DWDocumentary/videos)

*C#:*

- https://itvdn.com/ru/blog/article/150-questions-net-developer
  
- https://metanit.com/sharp/interview/

- https://www.guru99.com/c-sharp-interview-questions.html

- https://www.c-sharpcorner.com/UploadFile/puranindia/C-Sharp-interview-questions/

- https://hackr.io/blog/c-sharp-interview-questions

- http://a4academics.com/interview-questions/52-dot-net-interview-questions/417-c-oops-interview-questions-and-answers

- https://www.softwaretestinghelp.com/c-sharp-interview-questions/

- https://tproger.ru/articles/problems/

- https://cmsmagazine.ru/journal/items-80-problems-with-it-interviews/

- https://habr.com/ru/post/351874/

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
- https://ru.reactjs.org/

*Java-Script:*
https://learn.javascript.ru/

*Unit-testing:*

- https://gist.github.com/vertigra/696e9d92dc72070584e556e2169e850d

- https://habr.com/ru/post/116372/

- https://www.maxshulga.ru/2012/03/mock-vs-stub.html

*Redux:*
- https://habr.com/ru/company/mailru/blog/303456/
-----------------------------
Табличная селективность или селективность строк – соотношение количества строк, возвращаемых запросом к общему количеству строк в таблице.

Индексная селективность - отношение числа строк соответствующих конкретному ключевому значению к общему числу строк в индексе.
 
Селективность индекса – это показатель того, сколько строк от общего числа приходится на одно ключевое значение индекса.
Селективность хороша, если мало строк имеют одинаковые ключевые значения.

Характеристика кластеризованного и некластеризованного индекса:
- https://docs.microsoft.com/ru-ru/sql/relational-databases/indexes/clustered-and-nonclustered-indexes-described
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

-------------
webpack — это сборщик модулей JavaScript с открытым исходным кодом[2][3][4][5][6]. Он создан в первую очередь для JavaScript, но может преобразовывать внешние ресурсы, такие как HTML, CSS и изображения, если включены соответствующие загрузчики[7]. webpack принимает модули с зависимостями и генерирует статические ресурсы, представляющие эти модули[8].

Babel - это транспайлер, который переписывает код современного стандарта Javascript (ES2015) на более поздний. Транспайлер - это программа, позволяющая менять исходный код одной программы на эквивалентный исходный код на другом языке.

package-lock - Lock-файл — это моментальный снимок всего дерева зависимостей, включающий все пакеты и их установленные версии.

- Package manager (npm, yarn)
- Bundler (Webpack, Rollup, Parcel, Browserify)
- Транспилеры (Babel, SWC)
- Task Runner (Gulp, Grunt)
- Линтеры (ESlint, JSlint, TSLint, Prettier)
- Static Type Checker/Language (Flow, Typescript)
- CSS-препроцессоры (PostCSS, SASS, LESS, Stylus)
- JS -> CSS (JSS, styled components)
- CSS Frameworks (MaterialUI, Bootstrap)
  
Webpack:
- Горячая загрузка
- Ленивая загрузка
- Loader'ы
- Плагины (ESLintPlugin)
  
Visual Studio Code Plugins:
- Auto Close Tag
- Auto Rename Tag
- Code Spell Checker
- CSS Peek
- Live Server
- Path Autocomplete


Сравнение JS Framework'ов:
- https://habr.com/ru/post/476312/
- https://www.npmtrends.com/
  
Проверка совестимости:
- https://caniuse.com/
- https://statcounter.com/
- https://www.browserstack.com/

Best Practice:
- https://habr.com/ru/post/465685/

- https://github.com/cloudever/react-best-practices

----------------
ROAD MAPS:
- https://frontend-science.com/Middle_RoadMap.pdf
