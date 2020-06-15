# Асинхронные экшены в Redux

В Redux экшены синхронные. Для того что была возможность выполнять асинхронные экшены необходим middleware. Например, можно использовать `redux-thunk`. Для того что бы в Redux можно было использовать middleware нужно вызвать специальную функцию `applyMiddleware(...middleware)`.

- `applyMiddleware(...middleware)` - позволяет использовать middleware, для добавления какой-то новой функциональности в Redux, которая не предоставляется из коробки. middleware по структуре всегда такая `({ getState, dispatch }) => next => action`.
- 'redux-thunk' - middleware который проверяет является ли экшен функцией, и если является выполняет её, а если нет возвращает экшен. Реальный код 'redux-thunk':

  ```js
    function createThunkMiddleware(extraArgument) {
      return ({ dispatch, getState }) => (next) => (action) => {
        if (typeof action === 'function') {
          return action(dispatch, getState, extraArgument);
        }

        return next(action);
      };
    }
  ```

Пример:

```js
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';

const reducer = (state = [], action) { ... }

export const store = createStore(reducer, applyMiddleware(thunk));
```

## Ссылки

- [redux.js.org. Tutorial](https://redux.js.org/advanced/middleware)
- [redux.js.org. API](https://redux.js.org/api/applymiddleware)
- [Github. redux-thunk](https://github.com/reduxjs/redux-thunk)
