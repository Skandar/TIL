# void

Заметил, что typescript преобразует optional chaining в интересную строку, где используется выражение `void 0`.

```js
// исходный код
text?.include('Какой-то текст')

// транспилированный код
text === null || text === void 0 ? void 0 : text.include('Какой-то текст');
```

## Что такое void?

`void` вычисляет значение выражения справа от него и после этого **всегда** возвращает `undefined`. Есть несколько вариантов написания: `void 0` и `void(0)`, они взаимозаменяемы.

## Преобразование `undefined` в `void 0`

TypeScript и Babel при транспиляции кода используют один и тот же полифилл для optional chaining, который меняет `undefined` на `void 0`. Зачем полифилл это делает? Есть несколько причин:

1. `void 0` короче `undefined`.
2. Для того чтобы перестраховаться от ситуаций, когда `undefined` "перезаписана", а `void 0` гарантированно вернёт `undefined` в изначальном виде.

Тут возникает вопрос: "А зачем это нужно, ведь начиная с ES5 `undefined` нельзя перезаписать?".

Да, действительно, всё так, но можно в отдельном скоупе определить переменную с именем `undefined` (`undefined` не является [зарезервированным словом в JS](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#reserved_keywords_as_of_ecmascript_2015)), и в такой ситуации `void` может быть полезен.

```js
(function() {
  var undefined = 'Сюрприз!';
  // "Сюрприз!" "string"
  console.log(undefined, typeof undefined);
  // undefined "undefined"
  console.log(void 0, typeof void 0);
})();

```

## Зачем ещё применяется void

### IIFE

Можно использовать IIFE не оборачивая функцию в круглые скобки:

```js
void function() {
  console.log('IIFE');
}();
```

### javascript:void(0)

Иногда можно встретить использование `void(0)` с псевдопротоколом `javascript:`:

- в `HTML` ссылках. Обычно можно встретить такое использование, в виде альтернативы обработчиков событий, например, для того чтобы при нажатии на ссылку ничего не происходило. При таком использовании браузер кинет в консоль ошибку о том, что при инлайне `javascript:` будут проблемы с CSP. Лучше так не делать:

  ```html
  <a href="javascript:void(0)">
    При клике на эту ссылку ничего не произойдёт
  </a>
  ```

- в закладках. Так можно делать в браузере bookmarklet, при нажатии на который выполняется указанный JS-код на текущей открытой странице:

    ```text
    // при нажатии на эту вкладку цвет фона текущей страницы меняется на красный
    javascript:void(document.body.style.backgroundColor='red')
    ```

### Стрелочные функции

Можно использовать для записи стрелочных функций без скобок и быть уверенным, что стрелочная функция всегда будет возвращать `undefined`:

  ```js
    // без скобок
    const onClick = () => void doSomething();

    // то же самое, но со скобками
    const onClick = () => {
      doSomething();
    }
  ```

## Ссылки

- [MDN. void](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/void)
- [MDN. undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)
- [babel-plugin-transform-undefined-to-void](https://babeljs.io/docs/en/babel-plugin-transform-undefined-to-void)
