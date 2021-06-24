# BigInt

bigint целочисленный примитивный тип не фиксированного размера. Имеет литерал `123n` и обёртку `BigInt(123)`.

`bigint` как и `number` может быть в разных системах счисления:

- 0xFFn
- 0b1101n
- 0o777n

## Чем `bigint` отличается от `number`

- Нет фиксированных лимитов размера числа. Размер адаптируется под число, чем больше число тем больше памяти оно занимает.
- Нельзя использовать в методах библиотеки `Math`.
- Нельзя совмещать в арифметических операциях (`+`, `-`, `*`, `/` и т.д.) с `number`. Предварительно числа нужно привести к какому-то общему типу, либо `bigint`, либо `number`.
- Не работает унарный оператор `+`, он специально не перегружен чтобы не ломать [совместимость c asm.js](https://github.com/tc39/proposal-bigint/blob/master/ADVANCED.md#dont-break-asmjs).
- Если в результате операции получится дробное число, у этого числа отбросится дробная часть.
- Беззнаковый побитовый сдвиг вправо `>>>` не работает [из-за бесконечного количества нулей слева и отсутствия бита фиксирующего знак числа](https://exploringjs.com/impatient-js/ch_bigints.html#bitwise-unsigned-right-shift-operator).
- При строгом сравнении (`===`)  `123n` не будет равен `123`, так как у них разные типы.
- Нет конструктора `BigInt`, выражение `new BigInt(123)` бросит ошибку.
- Формат json не поддерживает `bigint`, `JSON.stringify(123n)` бросит ошибку.

## FAQ

### Когда использовать `bigint` вместо `number`?

Когда работаем с целыми числа больше 53 бит.

### Что делать если нужно использовать числами больше 53 бит с дробной частью?

Если дробную часть нельзя откинуть то можно:

- Умножить число на такое значение, чтобы "запятая передвинулась" на столько порядков, которого было бы достаточно, чтобы дробной частью можно было пренебречь.
- Перевести число в строку.
- Ждать выхода [Decimal](https://github.com/tc39/proposal-decimal).

## Ссылки

- [MDN. BigInt](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt)
- [JavaScript for impatient programmers. Dr. Axel Rauschmayer](https://exploringjs.com/impatient-js/ch_bigints.html)
- [tc39. The BigInt Type](https://tc39.es/ecma262/multipage/ecmascript-data-types-and-values.html#sec-ecmascript-language-types-bigint-type)
- [tc39. BigInt Objects](https://tc39.es/ecma262/multipage/numbers-and-dates.html#sec-bigint-objects)
- [Github. tc39](https://github.com/tc39/proposal-bigint/blob/master/ADVANCED.md)
