# "use strict"

## Несколько моментов о строгом режиме

- Применяется или ко всему скрипту (пишется в начале скрипта), или к отдельной функции (пишется в начале функции). Если `"use strict"` добавлен не в начале скрипта/функции, он игнорируется.
- По умолчанию включён в классах и модулях.

## Ситуации при которых возникает исключение в строгом режиме

- Присвоение значения не объявленной ранее переменной (при отсутсвии `"use strict"` в глобальном объекте создаётся свойство соответствующее переменной).
- Присваивание значения глобальной переменной, защищенной от записи (например, `undefined` или `Infinity`).
- Присваивание значения свойству объекта, защищенному от записи.
- Присваивание значения свойству объекта, доступному только для чтения (геттеру).
- Задание нового свойства нерасширяемому объекту.
- Попытка удалить неудаляемое свойство объекта.
- Использование `delete` на имени переменной (например, `delete myVariable`).
- Задание несколько параметров функии с одинаковым именем.
- Использоывния синтаксиса восьмиричной системы счисления (например, `015` или `"\045"`). При использования суффикса `0o` ошибки не будет.
- Указание свойств у примитивных значений.
- Использование `with`.
- Использование `eval` или `arguments` как переменную или аргумент функции.
- Использование `arguments.callee`, `arguments.caller`, `anyFunction.caller` или `anyFunction.arguments`.
- Использование зарезервированных для ECMAScript 6 слов в названии переменных или аргументов (`implements`, `interface`, `let`, `package`, `private`, `protected`, `public`, `static` и `yield`).

## Ссылки

- [Strict mode](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Strict_mode)
- [Переход к строгому режиму](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Strict_mode/Transitioning_to_strict_mode)
