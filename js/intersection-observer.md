# Intersection Observer

Позволяет следить, за состоянием пересечения елементом и его родителем (или viewport). [Demo](https://codepen.io/skandar_sl/pen/gJeWXB)

```js
const element = document.querySelectorAll('.element');

const options = {
  // Родитель элемента. Если указано null, тогда роль родителя выполняет viewport
  root: null,

  // Внешние отступы родителя. Пересечение элементом родителя наступает
  // после преодоления этих отступов
  rootMargin: '0px',

  // Число или массив чисел, указывающий, при каком проценте видимости
  // целевого элемента должен сработать callback
  threshold: 1
};

const observer = new IntersectionObserver(handleIntersect, options);

observer.observe(element);
```

## Применение

- Линивая загрузка.
- Эффекты при скроле/смене слайда.
- Активация анимаций/видео/рекламы во время скрола.
- Подсчёт времени нахождения пользователя на странице в пределах определённого элемента (статьи или таблицы).
