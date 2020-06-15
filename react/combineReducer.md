# combineReducers

Redux предусматривает создание только одного Redux store с одним состоянием хранящимся в нём. Когда возникает необходимость в нескольких отдельных состояниях, можно создать эти состояния внутри глобального состояния с помощью `combineReducers(reducers)`. Эта функция принимает объект с несколькими редюсерами и возвращает состояние с формой этого объекта.

```js
import { combineReducers, createStore } from 'redux';

const commentsReducer = (state = [], action) { ... }
const usersReducer = (state = [], action) { ... }


const reducer = combineReducers({
  comments: commentsReducer,
  users: usersReducer
});

/*
  Состояние будет такой формы

  {
    comments: ...,
    users: ...
  }
*/
export const store = createStore(reducer);
```

## Ссылки

- [redux.js.org. Tutorial](https://redux.js.org/basics/reducers#splitting-reducers)
- [redux.js.org. API](https://redux.js.org/api/combinereducers)
