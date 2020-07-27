# Интерфейсы

Интерфейсы - это способ сгруппировать несколько аннотаций в одну именованную аннотацию. Они демонстрируют форму объекта (или его подтипов, например, функций) и особенности свойств этого объекта: тип, обязательно присутствует в объекте или нет, можно записывать и читать или только читать и т.д.

Интерфейс, не объект поэтому свойства интерфейса можно разделять точкой с запятой (рекомендуется), запятой или вообще ничего не ставить в конце аннотации.

Интерфейс доступен в любом месте файла, в не зависимости от того где он объявлен.

```ts
interface QuoteConfig {
  text: string;
}
```

## Не обязательные свойства

С помощью `?` в конце имени свойства можно показать, что это свойство не обязательно должно присутствовать в объекте.

Так же интерфейсы позволяют избежать ошибок при написании имени свойств, при попытке вызвать свойство, которое не указано в интерфейсе TypeScript выдаст ошибку.

```ts
interface QuoteConfig {
  text: string;
  quoteSymbols?: {  // Необязательное свойство
    start: string;
    end: string;
  };
}

function createQuote(config: QuoteConfig): string {
    let quote = config.text;
    // Тут TypeScript выдаст ошибку, из отсутствия свойства с таким именем в интерфейсе
    // Error: Property 'qouteSymbols' does not exist on type 'QuoteConfig'
    if (config.qouteSymbols) {
      quote = config.quoteSymbols.start + quote + config.quoteSymbols.end;
    }

    return quote;
}

const quoteOptions = { text: 'quote text', quoteSymbols: { start: '<<' , end: '>>' } };
let quote = createQuote(quoteOptions);
```

## Readonly свойства

Если известно, что какое-то свойство после инициализации объекта больше не будет меняться, то можно помочью TypeScript узнать об это, указав `readonly` перед именем свойства, и когда TypeScript встретит в коде попытку изменить это свойство он выдаст ошибку.

```ts
interface User {
  age: number;
  name: string;
  readonly id: string; // Это свойство нельзя перезаписать
}

const user: User = {
  id: 'aasas213',
  age: 25,
  name: 'Alex'
};

// Error: Cannot assign to 'id' because it is a read-only property
user.id = 'new_id';
```

## Проверка лишних свойств

При присвоении **литерала** объекта переменной или передачи его в качестве аргумента функции TypeScript выполняет проверку объекта на соответствие форме интерфейса, если будут найдены свойства, которых нет в интерфейсе TypeScript выдаст ошибку.

```ts
interface QuoteConfig {
  text: string;
  quoteSymbols?: {
    start: string;
    end: string;
  };
}

function createQuote(config: QuoteConfig): string {
  // ...
}

/*
  Error: Argument of type '{ text: string; color: string; }' is not assignable to parameter of type 'QuoteConfig'.
  Object literal may only specify known properties, and 'color' does not exist in type 'QuoteConfig'
*/
const quoteConfig: QuoteConfig = { text: 'quote text', color: 'red' };
let quote = createQuote(quoteConfig);

// Ошибка, так же будет если передать литерал в качестве аргумента функции
let quote = createQuote({ text: 'quote text', color: 'red' });
```

Есть несколько путей обойти проверку литерала:

- присвоить литерал переменной;
- использовать type assertion;
- использовать сигнатуру индекса.

```ts
// Присвоение литерала переменной. Если у переменной в типе явно не указан интерфейс, то ошибки нет
const quoteOptions = { text: 'quote text', color: 'red' };
let quote = createQuote({ text: 'quote text', color: 'red' } as QuoteConfig);

// Type assertion
let quote = createQuote({ text: 'quote text', color: 'red' } as QuoteConfig);

// Сигнатура индекса
interface QuoteConfig {
  text: string;
  quoteSymbols?: {
    start: string;
    end: string;
  };
  // Свойство любого типа у которого имя свойства типа string
  [propName: string]: any;
}
let quote = createQuote({ text: 'quote text', color: 'red' });
```

## Типы функции (Function Types)

Для определения типа функции с помощью интерфейса нужно указать в интерфейсе сигнатуру вызова. Имена параметров у функции могут не соответствовать именам аргументов в сигнатуре вызова.

```ts
interface SearchFunc {
  // Функция имеет 2 значения типа string и возвращает значение типа boolean
  (source: string, subString: string): boolean;
}

let mySearch: SearchFunc = function(src: string, sub: string): boolean {
  let result = src.search(sub);
  return result > -1;
}
```

## Индексируемые типы (Indexable Types)

У интерфейса можно указать сигнатуру индекса, которая показывает, с помощью индекса какого типа можно получить доступ к значению свойства объекта.

Это удобно использовать в тех случаях когда мы точно не знаем под каким индексом свойство будет добавлено, но знаем его сигнатуру. Можно использовать в качестве фолбэка.

```ts
interface StringArray {
  [index: number]: string;
}

let myArray: StringArray;
myArray = ["Bob", "Fred"];

let myStr: string = myArray[0];
```

Индексы могут быть типа `string` или `number`.

## Класс типы (Class Types)

Интерфейсы можно применять к классам, для этого класс должен его имплементировать. Интерфейсы описывают публичные поля и методы класса.

```ts
interface ClockInterface {
  currentTime: Date;
  setTime(d: Date): void;
}

class Clock implements ClockInterface {
  currentTime: Date = new Date();
  setTime(d: Date) {
    this.currentTime = d;
  }
  constructor(h: number, m: number) { }
}
```

## Наследование интерфейсов

Интерфейсы могут наследовать другие интерфейсы. Возможно наследовать несколько интерфейсов одновременно.

```ts
interface Shape {
  color: string;
}

interface QuoteConfig {
  text: string;
  quoteSymbols?: {
    start: string;
    end: string;
  };
}

interface NamedQuoteConfig extends QuoteConfig, Shape {
  author: string
}
```

## Интерфейс наследующий класс

Интерфейсы могут наследовать классы, перенимая у них свойства и методы, но не их реализацию. Интерфейс так же наследует приватные (private) и защищённые (protected) поля класса. Это значит что при создании интерфейса, который наследует класс с приватными или защищёнными полями, этот интерфейс может быть имплементирован только этим классом или его потомками.

```ts
class Control {
  // Это свойство есть только в этом классе
  private state: any;
}

interface SelectableControl extends Control {
  select(): void;
}

class Button extends Control implements SelectableControl {
  select() { }
}

// Не является классом Control или его потомком,
// поэтому TypeScript выдаст ошибку
// Error: Property 'state' is missing in type 'Image'.
class Image implements SelectableControl {
  private state: any;
  select() { }
}
```

## Ссылки

- [TypeScript Docs. Interfaces](https://www.typescriptlang.org/docs/handbook/interfaces.html)
