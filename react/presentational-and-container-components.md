# Presentational и Container Components

Для удобного написания React приложений был предложен паттерн, в котором компоненты разделяются на 2 вида: презентационный компонент (Presentational Component) и компонент-контейнер (Container Component).

|                  |  Presentational Components   |               Container Components                 |
|:----------------:|:----------------------------:|:--------------------------------------------------:|
| Назначение       | Как выглядит (вёрстка,стили) | Как работает (data fetching, обновление состояния) |
| Знает о Redux    | Нет                          | Да                                                 |
| Читает данные    | С пропсов                    | Подписывается на Redux состояние                   |
| Изменяет данные  | Вызывает колбэк из пропсов   | Диспатчит Redux actions                            |
| Способ написания | Руками                       | Обычно генерируется React Redux                    |

## Ссылки

- [redux.js.org. Usage with react](https://redux.js.org/basics/usage-with-react#presentational-and-container-components)
- [medium.com. Smart and dumb components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)
