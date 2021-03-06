# Vue Instance

При создание экземпляра Vue берёт объект, которые передан в конструктор и создаёт его копию, создаёт необходиммые геттеры и сеттеры и свойства внутри становятся реактивными. Добавленные свойства (обычным способом `vm.newProperty = 'value`) после создание экземпляра не будет обладать реактивностью.

## Создание экземпляра

При создании экземпляра Vue, в конструктор передаётся объект с такими свойствами:

- **`data`** - как следует из названия хранит данные (они не реактивны).
- **`methods`** - методы, вызываются при каждом перерендеринге.
- **`computed`** - по умолчанию геттер. В отличие от методов кеширует возвращаемое значение. Если реактивные свойства, которые используются внутри геттера не изменились, то при перерендеринге повторного вызова функции не происходит. Выполняет только синхронные операции. Так же при необходимости можно добавить setter. Для этого нужно указать свойство в котором будет храниться объект, в котором явно указывается геттер и сеттер.

  ```js
  // ...
  computed: {
    fullName: {
      // getter
      get: function () {
        return this.firstName + ' ' + this.lastName
      },
      // setter
      set: function (newValue) {
        var names = newValue.split(' ')
        this.firstName = names[0]
        this.lastName = names[names.length - 1]
      }
    }
  }
  // ...
  ```

- **`watch`** - каждое перерендеривание обновляет свойство за которым "следит". Использовать в случае асинхронных операция.

  ```js
  new Vue({
    el: '#demo',
    data: {
      response: ''
    },
    watch: {
      response(value) {
        setTimeout(() => {
          this.response = 'Succcess!';
        }, 2000);
      }
    }
  });
  ```

## Экземпляр

Когда экземпляр уже создан внутри него содержатся такие свойства:

- **`$data`** - ссылка на объект `data` в объекте используемом при создании экземпляра.
- **`$refs`** - объект с элементами DOM которые имеют ссылки. Ссылку можно добать используя специальный атрибут `ref` (это не HTML атрибут).

  ```html
  <span ref="someUnicRefference">Text</span>
  ```

  При измении состояния элементов с помощью `ref` нужно помнить, что ссылки создаются функцией `render`, поэтому их не получится использовать при первичной отрисовке - на тот момент они ещё не существуют. Объект `$refs` не является реактивным, поэтому не нужно его использовать в шаблонах для связывания данных.

  Объект `$refs` удобно использовать, когда нужно получить какой-то HTML элемент или компонент, на который указывает ссылка или его какие-то данные.

- **`$mount`** - если при создании экземпляра не был указано свойство `el`, то экземпляр будет непремонтированным. Для того что бы его примонтировать используется метод `$mount` (возвращающий экземпляр). В качестве аргумента он принимает элемент или селектор элемента к которому нужно примонтироваться. Если аргумент не указан, то шаблон будет отрисован вне документа и такой элемент можно вставить в нужное место с помощью стандартных средств управления DOM в JS.
