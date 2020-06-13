# Дескрипторы свойств

У свойств объекта есть такие дескрипторы:

- `configurable` - по умолчанию: `false`. Дескриптор отвечающий за право изменять дескрипторы (кроме, `value`) и удаление свойства из объекта. Если значение `false` менять дескрипторы у данного свойство нельзя. Это действие **необратимо**. Важный момент: даже если значение `configurable` `false`, значение `writable` можно поменять с `true` на `false` без ошибка. При попытке удалить свойство или поменять дескрипторы будет `TypeError` ошибка.
- `enumerable` - по умолчанию: `false`. Определяет показывается ли данное свойство при перечислении свойств объекта или нет. Например, при использовании метода `Object.keys(...)`.
- `value` - по умолчанию: `undefined`. Значение свойства.
- `writable` - по умолчанию: `false`. Определяет можно ли перезаписывать свойство. При попытке записать в неизменяемое поле  будет `TypeError` ошибка, в `use strict` моде.
- `get` - по умолчанию: `undefined`. Функция которая вызывается при попытке получить данные из свойства. Не может быть определена вместе с дескрипторами `value` и `writable`.
- `set` - по умолчанию: `undefined`. Функция, которая вызывается при попытке записать данные из в свойство. Не может быть определена вместе с дескрипторами `value` и `writable`.

Если свойство было определено с помощью `Object.defineProperty(...)` или `Object.defineProperties(...)`, и какие-то дескрипторы были явно не указаны, то их значение становится равным `false`.

- `Object.defineProperty(obj, prop, descriptor)` - определяет новое свойство у объекта или изменяет дескрипторы у уже существующих свойств.
`Object.defineProperties(obj, props)` - определяет группу новых свойство у объекта или изменяет дескрипторы у уже существующих свойств.
- `Object.getOwnPropertyDescriptor(obj, prop)` - возвращает дескрипторы указанного свойства.
- `Object.getOwnPropertyDescriptors(obj)` - возвращает все свойства со всеми дескрипторами в объекте.

- `Object.preventExtensions(obj)` - блокирует возможность добавления новых свойств в объект.
- `Object.isExtensible(obj)` - определяет, является ли объект расширяемым, можно ли добавлять новые свойства.
- `Object.seal(obj)` - блокирует возможность добавления новых свойств в объект, и выставляет всем свойствам `configurable: false`
- `Object.isSealed(obj)` - определяет, является ли объект "запечатанным".
- `Object.freeze(obj)` - `Object.seal(obj)` + выставляет всем свойствам `writable: false`
- `Object.isFrozen(obj)` - определяет, является ли объект "зафризенным".
- `Object.propertyIsEnumerable(prop)` - определяет, является ли указанное свойство перечисляемым".

## Ссылки

- [learn.javascript.ru. Свойства - геттеры и сеттеры](https://learn.javascript.ru/property-accessors)
- [MDN. Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
- [You Don't Know JS. this & Object Prototypes](https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/this%20%26%20object%20prototypes/ch3.md#property-descriptors)
