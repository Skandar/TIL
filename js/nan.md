# NaN

`NaN` (Not a Number) - значение обозначающее ошибку при выполнении числовых операций или неудачной попытке привести к числу.

Типом `NaN` является number.

```js
console.log(typeof NaN); // number
```

Получить `NaN` можно при

- попытке привести значения других типов к числу.

  ```js
  Number('Какой-то текст')
  Number(undefined)
  ```

- невозможности выполнении математических операций методами `Math`.

  ```js
  Math.log(-1)
  Math.sqrt(-1)
  ```

- выполнении математических операций с непосредственным использованием `NaN`.

  ```js
  NaN - 123
  7 ** NaN
  ```

Метод `indexOf` не найдёт `NaN` в массиве.

```js
[NaN].indexOf(NaN) // -1
```

Есть несколько способов проверки значение на `NaN`.

```js
const x = NaN;
console.log(Number.isNaN(x)); // true
console.log(Object.is(x, NaN)); // true
// пользуемся особенностью NaN, что при сравнении NaN с самим собой всегда будет false
console.log(x !== x); // true
```

## Ссылки

- [MDN. NaN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NaN)
- [JavaScript for impatient programmers. Dr. Axel Rauschmayer](https://exploringjs.com/impatient-js/ch_numbers.html#error-values)
