---
title: Методы HTTP запроса
slug: Web/HTTP/Reference/Methods
---

HTTP определяет множество **методов запроса**, которые указывают, какое желаемое действие выполнится для данного ресурса. Несмотря на то, что их названия могут быть существительными, эти методы запроса иногда называются _HTTP глаголами_. Каждый реализует свою семантику, но каждая группа команд разделяет общие свойства: так, методы могут быть {{glossary("safe", "безопасными")}}, {{glossary("idempotent", "идемпотентными")}} или {{glossary("cacheable", "кешируемыми")}}.

- [`GET`](/ru/docs/Web/HTTP/Reference/Methods/GET)
  - : Метод `GET` запрашивает представление ресурса. Запросы с использованием этого метода могут только извлекать данные.
- [`HEAD`](/ru/docs/Web/HTTP/Reference/Methods/HEAD)
  - : `HEAD` запрашивает ресурс так же, как и метод GET, но без тела ответа.
- [`POST`](/ru/docs/Web/HTTP/Reference/Methods/POST)
  - : `POST` используется для отправки сущностей к определённому ресурсу. Часто вызывает изменение состояния или какие-то побочные эффекты на сервере.
- [`PUT`](/ru/docs/Web/HTTP/Reference/Methods/PUT)
  - : `PUT` заменяет все текущие представления ресурса данными запроса.
- [`DELETE`](/ru/docs/Web/HTTP/Reference/Methods/DELETE)
  - : `DELETE` удаляет указанный ресурс.
- [`CONNECT`](/ru/docs/Web/HTTP/Reference/Methods/CONNECT)
  - : `CONNECT` устанавливает "туннель" к серверу, определённому по ресурсу.
- [`OPTIONS`](/ru/docs/Web/HTTP/Reference/Methods/OPTIONS)
  - : `OPTIONS` используется для описания параметров соединения с ресурсом.
- [`TRACE`](/ru/docs/Web/HTTP/Reference/Methods/TRACE)
  - : `TRACE` выполняет вызов возвращаемого тестового сообщения с ресурса.
- [`PATCH`](/ru/docs/Web/HTTP/Reference/Methods/PATCH)
  - : `PATCH` используется для частичного изменения ресурса.

## Спецификации

| Спецификация                            | Название                                                      | Комментарий                                                        |
| --------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------------ |
| {{RFC("7231", "Request methods", "4")}} | Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content | Определение GET, HEAD, POST, PUT, DELETE, CONNECT, OPTIONS, TRACE. |
| {{RFC("5789", "Patch method", "2")}}    | PATCH метод для HTTP                                          | Определение PATCH.                                                 |

## Совместимость с браузерами

{{Compat}}

## Смотрите также

- [HTTP заголовки](/ru/docs/Web/HTTP/Reference/Headers)
