# Redux

Библиотека для упрощения работы с состоянием приложения.

## Несколько причин для выбора Redux

- большое количество данных в приложении, которые со временем будут меняться;
- нужен один "источник правды", состояние всего приложения хранится в одном месте);
- если содержать состояние всего приложения в компоненте верхнего уровня становится неудобно.

## Принципы

- единый "источник истины". Одно глобальное состояние;
- состояние не изменяется напрямую. Для изменения нужно вызвать метод `dispatch(action)`;
- `reducer` должен быть чистой функцией.

## Основные понятия

- **Action** - объект в котором описано какое действие над состоянием нужно выполнить и данные для это действия. Для уменьшения вероятности допустить ошибку при наборе поля `type` строку можно поместить в отдельную переменную и создать функцию `action creator` которая будет принимать значение и возвращать `action`.

  ```js
    // Action type
    const ADD_TODO = 'ADD_TODO';

    function actionCreator(text) {
      return {
        type: ADD_TODO, // описывает какое действие нужно выполнить с состоянием
        text: text // данные для действия
      };
    }
  ```

- **Reducer** - функция которая определяет что нужно сделать с состоянием. Принимает предыдущее состояние и `action`.

  ```js
    function todos(state = [], action) {
      switch (action.type) {
        case 'ADD_TODO':
          return state.concat([{ text: action.text, completed: false }])
        case 'REMOVE_TODO':
          return state.filter(todo => todo.text !== action.text);
        default:
          return state;
    }
  ```

  Reducer должен быть чистой функцией, и в нём нельзя:
  - мутировать его аргументы;
  - выполнять сайд эффекты (API вызовы, переходы между роутами);
  - вызывать "не чистые" функции (`Date.now()` или `Math.random()`)

- **Store** - объект в котором хранится состояние и методы для взаимодействия с ним. Есть такие методы:
  - `getState()` - возвращает состояние;
  - `dispatch(action)` - выполняет `action`;
  - `subscribe(listener)` - подписывает колбэк на обновление состояния. При подписке возвращается функция, которая позволяет отписаться. В React приложении пользователем не используется, эти функции выполняются в методе `connect` с библиотеки `react-redux`.

Работа с Redux происходит таким образом:

```js
  // Создаётся Redux store
  const store = createStore(reducer, initialState);

  // Подписывает на изменение состояния. Вызывает колбэк после каждого изменения состояния
  const unsubscribe = store.subscribe(() => console.log(store.getState());

  // Выполняется action, который возвращает функция actionCreator
  store.dispatch(actionCreator(value));

  // Берём состояние с Redux store
  console.log(store.getState());
```

## Ссылки

- [redux.js.org](https://redux.js.org/)
