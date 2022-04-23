- **RxJS** — это библиотека, используемая для создания асинхронных программ с использованием наблюдаемых последовательностей.
- Реактивная парадигма была сделана для обработки этих «событий» с обновлениями в режиме реального времени по всей программе. Реактивные программы структурированы вокруг событий, а не последовательного выполнения итеративного кода сверху вниз. Это позволяет им реагировать на триггерное событие независимо от того, на каком этапе находится программа.
- Одна из основных концепций реактивного программирования — синхронные и асинхронные данные. Короче говоря, синхронные данные доставляются по одному в кратчайшие сроки.
Асинхронные данные ожидают установленного события, а затем доставляются сразу через «обратный вызов». Асинхронные данные более популярны в реактивном программировании, потому что они хорошо соответствуют подходу парадигмы, основанному на событиях.
- Асинхронные данные более популярны в реактивном программировании, потому что они хорошо соответствуют подходу парадигмы, основанному на событиях.

**Преимущества:**
- Основное преимущество реактивного программирования заключается в том, что оно позволяет программе **реагировать на события независимо от текущей задачи программы**.
- **Высокая масштабируемость**
- **Чистый и читаемый**
- Легко добавить **поддержку нового события или ответа**
- Улучшенный пользовательский интерфейс благодаря **небольшому времени простоя**

--------------------------------------------------------
- Реактивная парадигма доступна для многих языков через реактивные расширения или Rx-библиотеки. Эти библиотеки представляют собой загружаемые API-интерфейсы, которые добавляют **поддержку основных реактивных инструментов, таких как наблюдатели и реактивные операторы**. 
- RxJS — это, в частности, инструмент функционального реактивного программирования **с шаблоном наблюдателя и шаблоном итератора**. Он также включает **адаптированную форму функций массива JavaScript (сокращение, отображение и т. Д.)** Для обработки асинхронных событий как коллекций.

- **Наблюдаемые** — это части нашей программы, которые генерируют данные с течением времени. **Данные наблюдаемого** — это поток значений, которые затем могут передаваться синхронно или асинхронно.
- **Конвейеры данных** — это последовательный ряд преобразований, через которые проходят все данные в потоке, прежде чем они будут представлены пользователю. Эти преобразования могут применяться ко всем проходящим данным, например, чтобы сделать поток более читаемым для пользователя.
--------------------------------------------------------
```
const { from } = require(‘rxjs’);
```

```
const { tap, filter, map } = require(‘rxjs/operators’);
```
--------------------------------------------------------
```
of(1,2,3).pipe(
  map(value => value * 2)
).subscribe({
  next: console.log
});
```

```
of(1, 2, 3).pipe(
  // пропускаем только нечетные значения
  filter(value => value % 2 !== 0),
  map(value = value * 2)
).subscribe({
  next: console.log
});
```
--------------------------------------------------------
```
const observable = new Observable((observer) => {
  observer.next(1);
  observer.next(2);
  observer.complete();
});
```
--------------------------------------------------------
**Array with foreach as Observable:**

```
const {Observable} = require(‘rxjs’)
const wrapArrayIntoObservable = arr => {
    return new Observable(subscriber => {
        for (let item of arr) {
            subscriber.next(item);
        }
    });
}
const data = [1, 2, 3, 4, 5];
const observable = wrapArrayIntoObservable(data);
observable.subscribe(val => console.log(‘Subscriber 1: ‘ + val));
observable.subscribe(val => console.log(‘Subscriber 2: ‘ + val));
```

```
// Output:
Subscriber1:1
Subscriber1:2
Subscriber1:3
Subscriber1:4
Subscriber1:5

Subscriber2:1
Subscriber2:2
Subscriber2:3
Subscriber2:4
Subscriber2:5
```
--------------------------------------------------------
**Конвейер данных RxJS:**

```
const { from } = require(‘rxjs’);
const { tap, filter, map } = require(‘rxjs/operators’);

const arrayDataObservable$ = from([1, 2, 3, 4, 5]);

const dataPipeline = arrayDataObservable$.pipe(
    tap(val => console.log(‘Value passing through the stream: ‘ + val)),
    filter(val => val > 2),
    map(val => val * 2)
)

const subscribeToBaseObservable = subscriberName => {
    return arrayDataObservable$.subscribe(val => {
        console.log(subscriberName + ‘ received: ‘ + val);
    })
}

const subscribeToDataPipeline = subscriberName => {
    return dataPipeline.subscribe(val => {
        console.log(subscriberName + ‘ received: ‘ + val);
    })
}

const handleSubscriptionToBaseObservable = () => {
    const subscription1 = subscribeToBaseObservable(‘Subscriber1’);
    const subscription2 = subscribeToBaseObservable(‘Subscriber2’);
}

const handleSubscriptionToDataPipeline = () => {
    const subscription1 = subscribeToDataPipeline(‘Subscriber1’);
    const subscription2 = subscribeToDataPipeline(‘Subscriber2’);
}

// 1. Execute this function first
handleSubscriptionToBaseObservable();

// 2. Execute this function next
//handleSubscriptionToDataPipeline();
```

```
//raw output
Subscriber1 received:1
Subscriber1 received:2
Subscriber1 received:3
Subscriber1 received:4
Subscriber1 received:5
Subscriber2 received:1
Subscriber2 received:2
Subscriber2 received:3
Subscriber2 received:4
Subscriber2 received:5


//filtered output
Value passing through the stream:1
Value passing through the stream:2
Value passing through the stream:3
Subscriber1 received:6
Value passing through the stream:4
Subscriber1 received:8
Value passing through the stream:5
Subscriber1 received:10
Value passing through the stream:1
Value passing through the stream:2
Value passing through the stream:3
Subscriber2 received:6
Value passing through the stream:4
Subscriber2 received:8
Value passing through the stream:5
Subscriber2 received:10
```
--------------------------------------------------------
**Операторы создания RxJS:**

- **fromОператор** используется, чтобы обернуть массив, итератор в Observable. Этот оператор направляет программу к уже созданному набору данных, например к массиву, который затем используется для заполнения наблюдаемых значений.

```
const { from } = require('rxjs'); 
 
const DATA_SOURCE = [ 'String 1', 'String 2', 'Yet another string', 'I am the last string' ];
const observable$ = from(DATA_SOURCE)
 
observable$.subscribe(console.log)
```

```
// output
String 1
String 2
Yet another string
I am the last string
```

--------------------------------------------------------
**Операторы создания RxJS:**

- **of-Оператор** является вторым наиболее распространенным Творения оператора. ofОператор синтаксически подобен, fromно ofпринимает последовательные данные, а не итерационные данные, такие как массивы. Если он получает массив, ofпросто печатает массив как декларативное выражение. При обертывании наблюдаемых ofлучше всего использовать, если данные действительно имеют смысл в массиве.

```
const { of } = require('rxjs');


const DATA_SOURCE = [ 'String 1', 'String 2', 'Yet another string', 'I am the last string' ];
const observableArray$ = of(DATA_SOURCE)

console.log("Array data source")
observableArray$.subscribe(console.log)

console.log("\n")
console.log("Sequence data source")
const observableSequence$ = of('String 1', 'String 2', 'Yet another string', 'I am the last string')

observableSequence$.subscribe(console.log)
```

```
//output
Array data source
[ 'String 1',
  'String 2',
  'Yet another string',
  'I am the last string' ]

Sequence data source
String 1
String 2
Yet another string
I am the last string
```
