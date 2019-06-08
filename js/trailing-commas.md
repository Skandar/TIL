# “Лишние” запятые

JS изначально позволял использовать “лишнюю” запятую (trailing comma) в литералах массива `var list = [1, 2, 3,]`, в ECMAScript 5 появилась возможность использовать “лишнюю” запятую в литералах объекта `var obj = { a: 1, b: 2, c: 3, }`, в ECMAScript 2017 стало возможно использовать для параметров функций `function f(p,) {} `.



## Применение

- Дыры в массивах (плохая практика):

  ```js
  var arr = [1, 2, 3,,,];
  arr.length; // 5
  ```

- При вертикальном расположении значениях массива, полях объекта, параметрах/аргументах функции, позволяет избежать лишних движений при добавлении/удалении значения.

- Позволяет сделать diff немного чище (сверху без “лишней” запятой, снизу с запятой):![скриншот diff](https://efficientuser.files.wordpress.com/2018/08/gitliteral.png?w=636)

  

## Ссылки

- [ECMAScript – Trailing Commas](https://efficientuser.com/2018/08/22/ecmascript-trailing-commas/)

- [MDN. Trailing commas](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Trailing_commas)

  