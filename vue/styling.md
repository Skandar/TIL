# Стили и всё что с ними связано

В Vue есть несколько способовд динамически работы со стилями.

## Классы

Можно передать объект в котором `isActive` Boolean значение. При изменении `isActive` будет добавляться и удаляться класс.

```html
<div :class="{ active: isActive }"></div>
```

В объекте могут содержаться сколько угодно классов.

```html
<div
  class="static"
  v-bind:class="{ active: isActive, 'text-danger': hasError }"
></div>
```

Для более удобного менеджмента классов можно создать функцию, возвращающую объект с классами.

```js
data: {
  isActive: true,
  error: null
},
computed: {
  classObject: function () {
    return {
      active: this.isActive && !this.error,
      'text-danger': this.error && this.error.type === 'fatal'
    }
  }
}
```

Также список классов можно указать в виде массива.

```html
<div v-bind:class="[{ active: isActive }, errorClass]"></div>
```

## Inline стили

Необходимые стили можно сразу записывать в атрибут `style`.

```html
<div v-bind:style="styleObject"></div>
```

```js
data: {
  styleObject: {
    activeColor: 'red',
    fontSize: '30px'
  }
}
```

Vue автоматически добавляет префиксы свойствам, которые этого требуют.

Так же можно указать массив значений для CSS свойства. Рендерится последнее поддерживаемое браузером свойство.

```html
<div v-bind:style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
```
