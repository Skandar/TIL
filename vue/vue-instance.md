# Vue Instance

В инстансе Vue есть такие свойства:

- **`data`** - как следует из названия хранит данные (они не реактивны).

  ```js
  new Vue({ el: '#app', data: { message: 'Hello Vue.js!' } });
  ```

- **`methods`** - методы, вызываются при каждом перерендеринге.

```js
new Vue({
  el: '#app',
  data: {
    counter: 0
  },
  methods: {
    increment: function() {
      this.counter++;
    }
  }
});
```

- **`computed`** - по умолчанию геттер. В отличие от методов кеширует возвращаемое значение. Если реактивные свойства, которые используются внутри геттера не изменились, то при перерендеринге повторного вызова функции не происходит. Выполняет только синхронные операции.

```js
new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullName: function() {
      return this.firstName + ' ' + this.lastName;
    }
  }
});
```

Так же при необходимости можно добавить setter. Для этого нужно указать свойство в котором будет храниться объект, в котором явно указывается геттер и сеттер.

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
