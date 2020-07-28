# Типы

В TypeScript есть такие встроенные типы:

- `boolean` - булевое значение.

  ```ts
  let isDone: boolean = false;
  ```

- `number` - число.

  ```ts
  let decimal: number = 6;
  ```

- `string` - строка.

  ```ts
  let color: string = "blue";
  ```

- `array` - массив.

  ```ts
  // Массив с значениями любого типа
  let list: number[] = [1, 2, 3];
  // Массив чисел
  let list: Array<number> = [1, 2, 3];
  ```

- `tuple` (кортеж) - массив фиксированной величины со значениями известного типа.

  ```ts
  let x: [string, number] = ['hello', 10];
  ```

- `enum` (перечисление) - набор числовых констант. Если значение константы не указано явно, то ему присваивается число на 1 больше предыдущего значение, по умолчанию `enum` нумеруется начиная с 0. Значение может быть числом или выражением.

  ```ts
  // Red = 0, Green = 1, Blue = 2
  enum Color {Red, Green, Blue};
  // c = 1
  let c: Color = Color.Green;

  enum Color {Red = 5, Green, Blue}
  let c: Color = Color.Green;

  enum Color {Red = 1, Green = 2 + 11, Blue = 4}
  let c: Color = Color.Green;

  enum Color {Red = 1, Green, Blue}
  // colorName = Blue
  let colorName: string = Color[2];
  ```

- `any` - значение тип которого не известен во время компиляции (любой тип).

  ```ts
  let notSure: any = 4;
  notSure = "maybe a string instead";
  notSure = false;
  ```

- `unknown` - аналог `any`. Значение с типом `unknown` нельзя присвоить ничему, что имеет тип отличный от `unknown` и `any`, но значению с типом `unknown` можно присвоить значение любого типа. Над `unknown` нельзя выполнить операции, кроме `==`, `!=` и конкатенации со строкой с помощью `+`, а так же нельзя обращаться к свойствам внутри `unknown`.

- `void` - отсутствие какого либо типа. Обычно используется в функциях которые ничего не возвращают.

  ```ts
  function warnUser(): void {
    console.log("This is my warning message");
  }
  ```

- `null` и `undefined` - не очень часто используются. `null` и `undefined` можно присваивать любым типам. Если компиляция выполняется с ключом `--strictNullChecks` то `null` можно присваивать только переменной с типом `null`.

  ```ts
  let u: undefined = undefined;
  let n: null = null;
  ```

- `never` - тип определяет значение которого никогда не будет существовать. Например, функция всегда возвращает ошибку.

  ```ts
   // Ничего не возвращает, так как бросается исключение
  function error(message: string): never {
    throw new Error(message);
  }

  function fail() {
    return error("Something failed");
  }

  // Ничего не возвращает из-за вечного цикла
  function infiniteLoop(): never {
    while (true) {
    }
  }
  ```

- `object` - значение, которое не является примитивным, то есть любое, кроме: `number`, `string`, `boolean`, `bigint`, `symbol`, `null` или `undefined`.

- `symbol` - тип редко указывается явно.

## Type assertions

Когда известен более точный тип значение, компилятору можно его подсказать, и тогда он будет считать что значение имеет этот тип. Сделать это можно двумя способами: `<string>someValue` или `someValue as string`. В JSX разрешён только вариант с `as`.

```ts
let someValue: any = "this is a string";

let strLength: number = (<string>someValue).length;

// Или

let strLength: number = (someValue as string).length;
```

## Ссылки

- [TypeScript Docs. Basic Types](https://www.typescriptlang.org/docs/handbook/basic-types.html)
