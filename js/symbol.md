# Symbol

Symbol - примитив созданный с помощью функции `Symbol()`.

При создании символа ему можно задать описание, Symbol('asd'). Впоследствии оно будет доступна в свойстве `Symbol.description` (ES2019).

Основное применение:

- Уникальны ключи для свойств объекта.

  ```js
  const name = Symbol('name');
  const person = {
    age: 44,
    [Symbol('name')]: "Jon"
  }
  ```

- Способ создания значения для константы.

  ```js
  console.log(Symbol('name') === Symbol('name')) // false
  ```

## Примеры использования

Чаще всего использование `Symbol` можно встретить в библиотеках.

В реакте используется
https://github.com/facebook/react/blob/main/packages/shared/ReactSymbols.js#L35

Symbols

Тест кейсы V8
https://github.com/v8/v8/blob/master/test/mjsunit/es6/symbols.js

## Ссылки

[JavaScript for impatient programmers. Dr. Axel Rauschmayer](https://exploringjs.com/impatient-js/ch_bigints.html)
