- **Redux** - это менеджер состояний. Библиотека Redux — это способ управления состоянием приложения. Чаще всего его используют с React, но его возможности не ограничиваются одной этой библиотекой. В React - перемещение состояния вверх по дереву работает для простых приложений, но в более сложных архитектурах изменение состояния производится через свойства (props). Ещё лучше делать это через внешнее глобальное хранилище.

- В Redux общее состояние приложения представлено одним объектом JavaScript — state (состояние) или state tree (дерево состояний). Неизменяемое дерево состояний доступно только для чтения, изменить ничего напрямую нельзя. Изменения возможны только при отправке action (действия).
----------------------------------------------------
- **Действие (action)** — это JavaScript-объект, который лаконично описывает суть изменения. Единственное требование к объекту действия — это наличие свойства type, значением которого обычно является строка:

```
{
  type: 'CLICKED_SIDEBAR'
}
// подробности об изменении
{
  type: 'SELECTED_USER',
  userId: 232
}
```

- **Генераторы действий (actions creators)** — это функции, создающие действия:
```
function addItem(t) {
  return {
    type: ADD_ITEM,
    title: t
  }
}
```

```
dispatch(addItem('Milk'));
```

```
const dispatchAddItem = i => dispatch(addItem(i))
dispatchAddItem('Milk')
```

- **Редуктор (reducer)** — это чистая функция, которая вычисляет следующее состояние дерева на основании его предыдущего состояния и применяемого действия. Редуктор возвращает совершенно новый объект дерева состояний, которым заменяется предыдущий:

Редуктор — это всегда чистая функция, поэтому он **не должен**:

- мутировать аргументы;
- мутировать состояние. Вместо этого создаётся новое состояние с помощью Object.assign({}, ...);
- иметь побочные эффекты (никаких API-вызовов с какими-либо изменениями);
- вызывать нечистые функции. Это функции, результат которых зависит от чего-то кроме их аргументов (например, Date.now() или Math.random()).

```
(currentState, action) => newState
```

- **Хранилище (store)** — это объект, который:

- содержит состояние приложения;
- отображает состояние через getState();
- может обновлять состояние через dispatch();
- позволяет регистрироваться (или удаляться) в качестве слушателя изменения состояния через subscribe().

```
import { createStore } from 'redux'
import listManager from './reducers'
let store = createStore(listManager)
```
----------------------------------------------------
- **components:** место для хранения немых компонентов React. Этим компонентам все равно, используете ли вы Redux или нет.
- **containers:** каталог для компонентов Smart React, которые отправляют действия в хранилище Redux. Здесь будет происходить связь между redux и react.
- **actions:** создатели действий перейдут в этот каталог.
- **reducers:** каждый редуктор получает отдельный файл, и вы разместите всю логику редуктора в этом каталоге.
- **store:** логика для инициализации состояния и настройки хранилища будет здесь.