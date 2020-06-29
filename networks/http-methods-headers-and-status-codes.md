# HTTP. Заголовки, методы и коды ответа

HTTP - текстовый протокол передачи данных. Изначально был придуман для передали HTML, сейчас используется для передачи произвольного типа данных.

Отличительные особенности:

- Клиент серверная модель - клиент запрашивает у сервера ресурс, сервер отвечает.
- Простой - человекочитаемый текстовый формат.
- Расширяемый - для изменения функциональности просто добавить HTTP заголовки.
- Не имеет состояния - запросы никак не связаны друг с другом.
- Не зависит от транспортного протокола - единственное требование - надёжность.

![Базовый HTTP запрос](https://media.prod.mdn.mozit.cloud/attachments/2016/08/09/13687/5d4c4719f4099d5342a5093bdf4a8843/HTTP_Request.png)

Пример запроса

```http
GET / HTTP/1.1
Host: google.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:78.0) Gecko/20100101 Firefox/78.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.7,ru;q=0.3
Accept-Encoding: gzip, deflate
DNT: 1
Connection: keep-alive
Cookie: username=alex
Upgrade-Insecure-Requests: 1
Pragma: no-cache
Cache-Control: no-cache
```

Пример ответа

```http
HTTP/1.1 200 OK
Age: 378358
Cache-Control: max-age=604800
Content-Type: text/html; charset=UTF-8
Date: Thu, 25 Jun 2020 10:30:25 GMT
Etag: "3147526947+ident"
Expires: Thu, 02 Jul 2020 10:30:25 GMT
Last-Modified: Thu, 17 Oct 2019 07:18:26 GMT
Server: ECS (nyb/1D11)
Vary: Accept-Encoding
X-Cache: HIT
Content-Length: 1256

<!DOCTYPE html ...
```

## Заголовки

Что бы изменить функциональность запроса/ответа, достаточно добавить нужные заголовки. Популярные заголовки:

- `Host` - доменное имя сервера (например, example.com).
- `User-Agent` - UA браузера.
- `Referer` - страница с которой выполнен переход (написано с ошибкой).
- `Cookie` - куки, которые ранее были выданы сервером.
- `Range` - определяет часть документа, которую сервер должен вернуть.
- `Cache-Control` - содержит инструкции по поводу кеширования.
- `If-Modified-Since` - сервер возвращает запрошенный ресурс, только в том случае если он был изменён после указанной в заголовке даты.
- `Connection` - определяет должно соединение быть разорвано или остаться открытым. Не используются в HTTP/2 для таких целей, т.к. эта информация там передаётся другими способами.
- `Accept` - определяет какой тип контента клиент может понять (например, `text/html`).
- `Accept-Encoding` - алгоритм кодирования который понимает клиент, обычно это подразумевает алгоритм сжатия (например, `gzip`).
- `Accept-Language` - содержит указания на то какой язык понимает клиент и предпочтения по локали (например, `ru` иди `en-US`).

## Методы

Для взаимодействия с сервером в HTTP есть такие методы:

- `GET` - запрашивает представление ресурса. Запросы с использованием этого метода могут только извлекать данные.
- `HEAD` - запрашивает ресурс так же, как и метод GET, но без тела ответа.
- `POST` - используется для отправки сущностей к определённому ресурсу. Часто вызывает изменение состояния или какие-то побочные эффекты на сервере.
- `PUT` - заменяет все текущие представления ресурса данными запроса.
- `DELETE` - удаляет указанный ресурс.
- `CONNECT` - устанавливает "туннель" к серверу, определённому по ресурсу.
- `OPTIONS` - используется для описания параметров соединения с ресурсом.
- `TRACE` - выполняет вызов возвращаемого тестового сообщения с ресурса.
- `PATCH` - используется для частичного изменения ресурса.

## Коды состояния

Что бы понять как сервер отреагировал на запрос, в ответ добавляется код состояния. Все коды состояния принадлежат к одному из 5 диапазонов:

- 100 – 199 - Информационные
- 200 - 299 - Успешные
- 300 - 399 - Перенаправления
- 400 - 499 - Клиентские ошибки
- 500 - 599 - Серверные ошибки

Самые популярные:

- `200 OK` - успешный запрос. Если клиентом были запрошены какие-либо данные, то они находятся в заголовке и/или теле сообщения.
- `206 Partial Content` - сервер удачно выполнил частичный `GET`-запрос, возвратив только часть сообщения. В заголовке `Content-Range` сервер указывает байтовые диапазоны содержимого. Особое внимание при работе с подобными ответами следует уделить кэшированию.
- `301 Moved Permanently` - запрошенный ресурс был окончательно перенесен на новый URI, указанный в поле `Location` заголовка. Некоторые клиенты некорректно ведут себя при обработке данного кода.
- `302 Found` - запрошенный документ временно доступен по другому URI, указанному в заголовке в поле `Location`.
- `304 Not Modified` - сервер возвращает такой код, если клиент запросил документ методом `GET`, использовал заголовок `If-Modified-Since` или `If-None-Match` и документ не изменился с указанного момента. При этом сообщение сервера не должно содержать тела.
- `400 Bad Request` - сервер обнаружил в запросе клиента синтаксическую ошибку.
- `401 Unauthorized` - доступа к запрашиваемому ресурсу требуется аутентификация. В заголовке ответ должен содержать поле WWW-Authenticate с перечнем условий аутентификации. Иными словами, для доступа к запрашиваемому ресурсу клиент должен представиться, послав запрос, включив при этом в заголовок сообщения поле Authorization с требуемыми для аутентификации данными. Если запрос уже включает данные для авторизации, ответ 401 означает, что в авторизации с ними отказано.
- `403 Forbidden` - Сервер вернул ошибку `403` при попытке просмотра каталога «cgi-bin», доступ к которому был запрещён сервер понял запрос, но он отказывается его выполнять из-за ограничений в доступе для клиента к указанному ресурсу. Иными словами, клиент не уполномочен совершать операции с запрошенным ресурсом. Если для доступа к ресурсу требуется аутентификация средствами HTTP, то сервер вернёт ответ `401`, или 407 при использовании прокси. В противном случае ограничения были заданы администратором сервера или разработчиком веб-приложения и могут быть любыми в зависимости от возможностей используемого программного обеспечения. В любом случае серверу следует сообщить причины отказа в обработке запроса. Наиболее вероятными причинами ограничения может послужить попытка доступа к системным ресурсам веб-сервера (например, файлам `.htaccess` или `.htpasswd`) или к файлам, доступ к которым был закрыт с помощью конфигурационных файлов, требование аутентификации не средствами HTTP, например, для доступа к системе управления содержимым или разделу для зарегистрированных пользователей либо сервер не удовлетворён IP-адресом клиента, например, при блокировках.
- `404 Not Found` - самая распространённая ошибка при пользовании Интернетом, основная причина — ошибка в написании адреса Web-страницы. Сервер понял запрос, но не нашёл соответствующего ресурса по указанному URL. Если серверу известно, что по этому адресу был документ, то ему желательно использовать код `410`. Ответ `404` может использоваться вместо `403`, если требуется тщательно скрыть от посторонних глаз определённые ресурсы.
- `500 Internal Server Error` - любая внутренняя ошибка сервера, которая не входит в рамки остальных ошибок класса.
- `502 Bad Gateway` - сервер, выступая в роли шлюза или прокси-сервера, получил недействительное ответное сообщение от вышестоящего сервера.
- `503 Service Unavailable` - сервер временно не имеет возможности обрабатывать запросы по техническим причинам (обслуживание, перегрузка и прочее). В поле `Retry-After` заголовка сервер может указать время, через которое клиенту рекомендуется повторить запрос. Хотя во время перегрузки очевидным кажется сразу разрывать соединение, эффективней может оказаться установка большого значения поля `Retry-After` для уменьшения частоты избыточных запросов.
- `504 Gateway Timeout` - сервер в роли шлюза или прокси-сервера не дождался ответа от вышестоящего сервера для завершения текущего запроса.

## Ссылки

- [Web Security - Lecture 02 - HTTP, Cookies, Sessions](https://www.youtube.com/watch?v=zhnQFQ2qFtA)
- [MDN. HTTP request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
- [MDN. HTTP request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
- [Wikipedia. Список кодов состояния HTTP](https://ru.wikipedia.org/wiki/Список_кодов_состояния_HTTP)