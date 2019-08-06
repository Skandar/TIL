# Template Syntax

Vue работает c html, как с шаблонами, добавляя в него свои конструкции. Значение в скобках интерполируется (на выходе получается строка).

```html
<span>Message: {{ msg }}</span>
```

## Интерполяция только один раз

В Vue используются дерективы (что-то вроде атрибутов у тега) начинающиеся с `v-` (ну или со знака в сокращённой версии `@`, `:`).

Если необходимо выполнить интерполяцию 1 раз (после изменения свойства msg, значение в html повторно не интерполируется), используется директива `v-once`.

## Вывод html

```html
<span v-once>This will never change: {{ msg }}</span>
```

Для использования html используется директива `v-html` в которую передаётся значение, которое необходимо вставить внутри тега.

```html
<p>Using v-html directive: <span v-html="rawHtml"></span></p>
```

## Привязывание значения к тегу

Для использования html используется директива `v-bind:` (или `:`) в которую передаётся значение атрибута, которму присваивается значение.

```html
<p>Using v-html directive: <span v-bind:title="title"></span></p>
```

## Обработчики событий

Для обрабатывания событий используется директива `v-on:` (или `@`) после которой следует название события которое слушается (`click`, `keyup` и т.д.) и передаётся метод обработчик события.

```html
<div id="app">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Reverse Message</button>
  <!-- <button @:click="reverseMessage">Reverse Message</button> -->
</div>
```

```js
var app5 = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function() {
      this.message = this.message
        .split('')
        .reverse()
        .join('');
    }
  }
});
```

В Vue есть возможность передавать в обработчик событий значение по умолчанию, так же есть зарезервированное значение `$event` в котором содержится объект события.

```html
<div id="app">
  <p>{{ message }}</p>
  <button v-on:click="clickEventHandler">
    Reverse Message
  </button>
</div>
```

## Модификаторы событий

Для придания особого поведения обработчику событию (например, что бы остановить "всплытие" события или действие по умолчанию) есть модификаторы `stop` (останавливает всплытие), `prevent` (останавливает действие по умолчанию) и т.д.

```html
<div id="app">
  <p>{{ message }}</p>
  <button v-on:click="btnClickHandler">
    Reverse Message
    <span v-on:click.stop></span>
  </button>
  <form @submit.prevent="formSubmitHandler">
    ...
  </form>
</div>
```

## Формы

Для связывания данных с тегом и добавления отслеживания событий у `input`, `checkbox`, `radio` и `textarea` есть деректива `v-model`.

```html
<div id="app">
  <input type="text" v-model="message" />
  <p>{{ message }}</p>
</div>
```
