# Сортировка пузырьком (Bubble sort)

Простой алгоритм сортировки, который сравнивает каждое значение с последующим и в случае если текущее значение больше последующего меняет эти значения местами. После того как сравняться все числа в конце окажется самое большое число. После этого процесс повторяется. Это напоминает процесс всплытия пузырька в воде, благодаря чему этот метод сортировки и получил такое название.

![Визуализация сортировки](https://camo.githubusercontent.com/383b23979d4d7f279f8fb285b36bcdd357b10a35/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f632f63382f427562626c652d736f72742d6578616d706c652d33303070782e676966)

## Сложность

| Лучший результат |    В среднем        | Худший              | Память    | Стабильный |
| :--------------: | :-----------------: | :-----------------: | :-------: | :--------: |
| n                | n<sup>2</sup>       | n<sup>2</sup>       | 1         | Да         |

## Реализация

```js
const bubbleSort = arr => {
  let isSorted = false;
  let end = arr.length - 1;
  while(!isSorted) {
    isSorted = true;
    for (let i = 0; i < end; i++) {
      if (arr[i] > arr[i + 1]) {
        const tmp = arr[i + 1];
        arr[i + 1] = arr[i]
        arr[i] = tmp;

        isSorted = false;
      }
    }
    end--;
  }

  return arr;
};
```

## Ссылки

- [Github. trekhleb/javascript-algorithms](https://github.com/trekhleb/javascript-algorithms/tree/master/src/algorithms/sorting/bubble-sort)
- [visualgo.net](https://visualgo.net/ru/sorting)
