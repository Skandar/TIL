# DNS

DNS позволяет по домену, получить ip адрес ресурса. Вводя URL (например, **example.com**) в адресную строку браузера и нажимая Enter происходят такие операции:

1. Браузер запрашивает у DNS ip адрес нужного ресурса.
2. DNS отправляет запрос Root nameserver. Root nameserver возвращает IP адрес TLD nameserver (сервера имён домена верхнего уровня, "com").
3. DNS отправляет запрос TLD nameserver. TLD nameserver возвращает IP адрес Domain nameserver.
4. DNS отправляет запрос Domain nameserver. Domain nameserver возвращает IP адрес ресурса.
5. DNS возвращает браузеру IP ресурса.

## Перехват DNS (DNS hijacking)

Атакующий меняет DNS записи цели, что бы они указывали на его собственный IP адрес и все посетители сайта направляются на сервер атакующего.

Мотивы атакующего:

- Фишинг.
- Получение прибыли через рекламу, майнинг криптовалюты и т.д.

Векторы атаки:

- Малварь меняет локальные DNS настройки пользователя.
- Взлом DNS.
- Взлом роутера.
- Взлом DNS nameserver.
- Скоспрометировать учетная запись у провайдера DNS.

## Ссылки

- [Web Security - Lecture 02 - HTTP, Cookies, Sessions](https://www.youtube.com/watch?v=zhnQFQ2qFtA)
- [wikipedia.org. DNS](https://ru.wikipedia.org/wiki/DNS)
