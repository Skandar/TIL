# Hoisting

Hoisting позволяет использовать переменные/функции до их определения в пределах области видимости.

|            | Область видимости (scope) | Когда можно использовать              | Дублирование имени в пределах одной области видимости | Свойство в global |
| :--------- | :------------------------ | :------------------------------------ | :---------------------------------------------------- | ----------------- |
| `const`    | Блок                      | После объявления (TDZ)                | `✘`                                                   | `✘`               |
| `let`      | Блок                      | После объявления (TDZ)                | `✘`                                                   | `✘`               |
| `function` | Блок (в `strict` моде)    | В начале области видимости            | `✔`                                                   | `✔`               |
| `class`    | Block                     | После объявления (TDZ)                | `✘`                                                   | `✘`               |
| `import`   | Модуль                    | В начале области видимости            | `✘`                                                   | `✘`               |
| `var`      | Функция                   | В начале области видимости (частично) | `✔`                                                   | `✔`               |

TDZ (_temporal dead zone_) - время/пространство между началом области видимости и выполнением присвоения.

```js
{
  console.log(x); // ReferenceError
  const x;
}
```

## Ссылки

- [Unpacking hoisting](http://2ality.com/2019/05/unpacking-hoisting.html)