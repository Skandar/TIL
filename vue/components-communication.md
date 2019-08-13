# Коммуникация компонентов

Существует несколькоко способов выполнить коммуникацию между компонентами, в зависимости от их положении в иерархии относительно друг друга.

## Props

Для передачи данных от родительского компонента к дочернему существует свойство `props` (входной параметр). Это свойство указывается у дочернего элемента, и служит аналогом интерфейса для родительского компонента (определяет что нужно передать, обязательность этого входного параметра, какого типа данных должен быть).

Для передачи статических данных используется аргумент c именем входного параметра (например, `size="100px"`), а для передачи динамических данных нужно использовать директиву связывания `:text="textData"`

```html
<!-- Родительский компонент -->
<template>
  <text size="100" :text="textData" />
</template>
```

```html
<!-- Дочерний компонент -->
<template>
  <button :size="className">{{ text }}</button>
</template>

<sctipt>
export default {
  props: ["text", "size"]
}
</script>
```

Так же есть возможность валидировать входные параметры:

```js
export default {
  props: {
    // Значение указывает на тип данных, который должны быть в props
    text: String,
    size: [String, Array]
  }
};
```

При необходимости у входного параметра можно указать:

- `type` - тип входных данных
- `required` - обязательное указание этого входного параметра в родительском компоненте.
- `default` - значение по умолчанию

```js
export default {
  props: {
    // Значение указывает на тип данных, которые должны быть в props
    text: {
      type: String,
      // Указывает что props обязательно должен быть передан
      required: true
    }
    size: {
      type: [String, Array],
      // Значение по умолчанию, в случае если ничего не передано
      default: 300
    }
  }
}
```

## Дочерний компонент --> Родительский компонент

Для передачи данных из дочернего компонента родительскому можно воспользоваться следующими способами:

- Передать во входном параметре callback, который меняет что-то в родительском элементе при вызове.
- Пользовательские события - генерируя событие с помощью метода `$emit`:

  ```html
  <label>
    {{ label }}
    <input
      v-bind="$attrs"
      v-bind:value="value"
      v-on:input="$emit('input', $event.target.value)"
    />
  </label>
  ```

## Комуникация между любыми компонентами

Во Vue по умолчанию нет возможности комуницировать между с помощью `$emit`, но можно воспользоваться подходом, который называется "Event bus". Его суть в том что нужно создать отдельныго экземпляр, который будет импортирован всеми компонентами, между которыми необходима связь, определить пользовательское событие (с помощью `$emit`) и добавить слушатели событий в других компонентах (в хуке жизненного цикла `create`).