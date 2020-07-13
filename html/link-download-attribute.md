# download атрибут у ссылки

Позволяет при клике на ссылку сразу скачивать файл.

Польза:

- Меньше действий для сохранения файла (улучшает UX).
- Позволяет переопределить имя файла.

Для корректной работы файл должен быть на этом же источнике (same origin).

```html
<!-- Сохранит изображение "image.png" с именем "best-image.png" -->
<a download="best-image.png" href="/image.png">
  <img src="/image.png" alt="image">
</a>
```

## Ссылки

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#download)
