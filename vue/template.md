# Шаблоны

В Vue есть возможность создавать шаблоны, указывая HTML теги в виде строки в свойстве `template`.

```js
const vm = new Vue({
  template: `<button>Button</button>`
});

vm.$mount();

document.querySelector('#app').appendChild(vm.$el);
```
