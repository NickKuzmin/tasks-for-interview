- JS Techincal tasks: https://github.com/bakugod/interview-tasks/blob/master/algorithmic-part.md
---------------------------
- Console API methods (assert, count, dir, group, time, trace):
https://developer.mozilla.org/en-US/docs/Web/API/Console

*Difference of using async / await vs promises:*
- https://habr.com/ru/company/ruvds/blog/326074/

*Node.js. Event Loop:*
- https://habr.com/ru/post/479062/

- Async library: https://caolan.github.io/async/v3/
- Debounce/Throttling https://css-tricks.com/debouncing-throttling-explained-examples/

---------------------------
**Библиотеки:**
- Stampit: https://github.com/stampit-org/stampit
---------------------------
- Call Stack, Web APIs, Render Queue, Callback Queue
- 16.000 methods - callstack overvflow
- Asm.js
- WebAssembly
- Babel 
- Traceur
---------------------------
```
function Vehicle(maxSpeed) {
    this.maxSpeed = maxSpeed;
}

Vehicle.prototype.maxSpeed = function() {
    return this.maxSpeed;
}

function Car(maxSpeed) {
    Vehicle.call(this, maxSpeed);
}

Car.prototype = new Vehicle();
```
---------------------------
```
Object.seal
Object.freeze
Object.createProperty
```
---------------------------
Краткий список новых возможностей включает в себя:

- Let (лексическая) и const (неизменяемая) привязки
- Стрелочные функции (короткие анонимные функции) и лексическое this
- Классы (синтаксический сахар поверх прототипов)
- Улучшения объектных литералов (вычисляемые ключи, укороченные определения методов и т.д.)
- Шаблонные строки
- Промисы
- Генераторы, итерируемые объекты, итераторы и for..of
- Параметры функций по умолчанию и оператор rest
- Spread-синтакис
- Деструктуризация
- Модульный синтаксис
- Новые коллекции (Set, Map, WeakSet, WeakMap)
- Прокси и Reflect
- Тип данных Symbols
- Типизированные массивы
- Наследование классов
- Оптимизация хвостовой рекурсии
- Упрощённая поддержка Unicode
- Двоичные и восьмеричные литералы
---------------------------
- необязательный атрибут ```src```, принимающий в качестве значения адрес к файлу со скриптом.
- необязательный атрибут ```charset```, используемый вместе с src для указания используемой кодировки внешнего файла.
- необязательный атрибут ```defer``` указывает, что получение скрипта происходит асинхронно, но выполнение следует отложить до тех пор, пока страница не будет загружена целиком.
- необязательный атрибут ```async``` указывает, что получение скрипта происходит асинхронно, а выполнение будет произведено сразу по завершении скачивания. Очерёдность выполнения скриптов не гарантируется.
---------------------------
- **prototype** is a property of a Function object. It is the prototype of objects constructed by that function.

- **__proto__** is an internal property of an object, pointing to its prototype. Current standards provide an equivalent Object.getPrototypeOf(obj) method, though the de facto standard __proto__ is quicker.You can find instanceof relationships by comparing a function's prototype to an object's __proto__ chain, and you can break these relationships by changing prototype.

