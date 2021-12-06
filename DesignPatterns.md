- https://ru.wikipedia.org/wiki/Шаблон_проектирования
- https://habr.com/ru/post/210288/
- https://refactoring.guru/ru/design-patterns/catalog
- https://javarush.ru/groups/posts/2267-patternih-proektirovanija-v-java
------------
**DESIGN PATTERNS in .NET:**

- **Abstract Factory** - pattern is used in the ADO.NET 2.0 infrastructure (DbProviderFactory class)
- **Builder** - DbConnectionStringBuilder, UriBuilder
- **Visitor Pattern** in **ExpressionVisitor** class (Syste.Linq.Expression namespace).
- **Adapter Pattern** in System.Web.Abstractions - wrap up various Web classes (HttpRequest, HttpResponse) in a more unit testable way - i.e. HttpResponseBase.
- **Factory Method** - **Activator.CreateInstance** - creates an instance of specified object.
- **Iterator** - all implementations of **IEnumerable**.
- **Prototype** - ICloneable interface with method Clone() is classic example of prototype.
- **NullObject** - String.Empty, EventArgs.Empty

------------
- **Порождающие паттерны (creational patterns)** - эти паттерны решают проблемы обеспечения гибкости создания объектов
- **Структурные паттерны (structural patterns)** - эти паттерны решают проблемы эффективного построения связей между объектами
- **Поведенческие паттерны (behavioral patterns)** - эти паттерны решают проблемы эффективного взаимодействия между объектами
------------
**Порождающие паттерны (creational patterns):**

- Абстрактная фабрика (abstract factory)
- Строитель (builder)
- Фабричный метод (factory method)
- Ленивая инициализация (lazy initialization)
- Объектный пул (object pool)
- Прототип (prototype)
- Одиночка (singleton)
- Пул одиночек (Multiton)
------------
**Структурные паттерны (structural patterns):**

- Адаптер (Adapter)
- Мост (Bridge)
- Компоновщик (Composite)
- Декоратор (Decorator)
- Фасад (Facade)
- Единая точка входа (Front controller)
- Приспособленец (Flyweight)
- Заместитель (Proxy)
------------
**Поведенческие паттерны (behavioral patterns):**

- Цепочка ответственности (Chain of responsibilily)
- Команда (Command)
- Интерпретатор (Interpreter)
- Итератор (Iterator)
- Посредник (Mediator)
- Хранитель (Memento)
- Null Object
- Наблюдатель (Observer)
- Слуга (англ.)русск.
- Specification (Specification)
- Состояние (State)
- Стратегия (Strategy)
- Шаблонный метод (Template method)
- Посетитель (Visitor)
- Simple Policy
- Event listener
- Single-serving visitor pattern
- Hierarchical visitor pattern 
