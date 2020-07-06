# Session hijacking

Пользователь использует не защищённое соединение (HTTP), атакующий слушает его трафик и берёт от туда куки для того что бы залогиниться на сайте в аккаунт пользователя.

Решение: всегда использовать HTTPS для передачи кук (`Set-Cookies: key=value; Secure`).

## Ссылки

- [Web Security - Lecture 03 - Session Attacks](https://youtu.be/QuhgjXKzfI8)
- [Wikipedia. Session hijacking](https://en.wikipedia.org/wiki/Session_hijacking)
