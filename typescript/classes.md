# Классы

TypeScript позволяет привнести недостающие в JavaScript возможности ООП, которые есть в других языках программирования.

```ts
class Greeter {
  greeting: string;
  constructor(message: string) {
    this.greeting = message;
  }
  greet() {
    return "Hello, " + this.greeting;
  }
}

let greeter = new Greeter("world");
```

## Модификаторы доступа

В TypeScript есть возможность определить область видимости у полей класса. Для этого нужно воспользоваться одним из модификаторов доступа:

- `public` (значение по умолчанию) - поле не имеет ограничений по доступу.
- `private` (или `#` в начале имени поля (ECMAScript приватное поле)) - поле не доступно за пределами класса.
- `protected` - поле доступно для класса в котором оно определено и для потомком этого класса.

| Доступ           | public | protected | private |
| :--------------- | :----: | :-------: | :-----: |
| класс            |   да   |    да     |   да    |
| потомок          |   да   |    да     |   нет   |
| экземпляр класса |   да   |    нет    |   нет   |

Нужно помнить, что модификаторы доступа (кроме `#`) работают только в TypeScript, и после компиляции в JavaScript, их не будет, так что разработчик пользующийся в последствии JavaScript кодом может не догадаться о том как планировалось использовать поля класса.

Конструктор может быть `protected`, тогда у этого класса нельзя создать экземпляр, но этот класс можно наследовать.

## Readonly модификатор

У поля класса можно указать модификатор `readonly`, что позволяет показать, что данное поле доступно только для чтения.

```ts
class Octopus {
  // Поле доступно только для чтения
  readonly name: string;
  constructor(name: string) {
    this.name = name;
  }
}
```

## Параметр свойства (parameter properties)

В TypeScript есть сокращение, которое позволяет избежать написания явного присваивания полю класса значения из конструктора. Для того что бы это сокращение сработало нужно у параметра конструктора явно указать модификатор доступа (`public`, `protected` или `private`) или модификатор `readonly`.

```ts
class Octopus {
  readonly name: string;
  constructor(
    name: string,
    private age: number // Сокращённый вариант
  ) {
    this.name = name; // Полный вариант
  }
}
```

## Абстрактный класс

Абстрактный класс - это класс шаблон, от которого наследуются другие классы. Для него нет возможности создать экземпляр класса. В отличии от интерфейса он может содержать детали имплементации класса.

Так же в абстрактном классе можно использовать абстрактные методы. У абстрактного метода нет имплементации, и класс который будет наследовать этот метод, должен его имплементировать.

```ts
abstract class Department {
  constructor(public name: string) {}

  printName(): void {
    console.log("Department name: " + this.name);
  }

  // Метод должен быть имплементирован в классе, который будет наследовать Department класс
  abstract printMeeting(): void;
}

class AccountingDepartment extends Department {
  constructor() {
    super("Accounting and Auditing");
  }

  // Имплементация абстрактного метода из абстрактного класса Department
  printMeeting(): void {
    console.log("The Accounting Department meets each Monday at 10am.");
  }
}
```

## Ссылки

- [TypeScript Docs. Classes](https://www.typescriptlang.org/docs/handbook/classes.html)
- [TypeScript Deep Dive. Classes](https://basarat.gitbook.io/typescript/future-javascript/classes)
- [Github. Typescript fundamentals](https://github.com/mike-works/typescript-fundamentals/blob/master/notes/4-class-basics.ts)
