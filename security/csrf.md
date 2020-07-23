# Cross-Site Request Forgery

При переходе на сайт злоумышленника анонимно отправляется запрос на сайт где пользователь зарегистрирован и был залогинен. Вместе с запросом отправляются куки пользователя благодаря чему сайт считает что это запрос от пользователя и он успешно выполняется.

## Защита

Добавлять ко всем кукам которые не отвечают за работу со сторонними сервисами атрибут `SameSite` со значением `Lax` или `Strict`.

## Ссылки

- [Web Security - Lecture 04 - Cross-Site Request Forgery, Same Origin Policy](https://www.youtube.com/watch?v=0-q69vAYSwo)
- [Cross-Site Request Forgery is dead!](https://scotthelme.co.uk/csrf-is-dead/)
