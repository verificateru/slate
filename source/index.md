---
title: Документация API verificate.ru

language_tabs:
  - shell

toc_footers:
  - <a href='http://www.verificate.ru'>Получить API токен</a>
  - <a href='http://github.com/tripit/slate'>Документация создана используя Slate</a>

includes:
  - errors

search: false
---

# Начало

Здравствуйте! 
Добро пожаловать на страницу документации API проекта [verificate.ru](http://www.verificate.ru/)! Используя наш API вы можете отправлять смс и звонки, получать их статусы и уведомления о текущем состоянии ресурсов.

<!-- Эта страница создана используя open source платформу для создания документации [Slate](http://github.com/tripit/slate). -->

# Описание

> Для авторизации используйте следующий код:

```shell
curl "api_endpoint"
  -H "Token: personal_token"
```

> Обязательно замените `personal_token` на ваш личный токен.

Для доступа к ресурсам API вам необходим токен. Токен это обычная строка-ключ, который выдается пользователю при регистрации и открывает ему доступ к функционалу нашего API. Получить токен вы можете после успешной [регистрации](http://verfificate.ru/auth/register) на странице [личного кабинета](http://verfificate.ru/private/profile).

Полученный ключ можно использовать передав ```HTTP``` заголовок с именем ```token```, либо добавив в тело запроса поле ```token```.

<aside class="warning">Для доступа к API, запрос <b>ОБЯЗАТЕЛЬНО</b> должен содержать токен.</aside>

# Смс сообщение

## Создание смс

```shell
curl "http://verificate.ru/api/v1/sms"
  -H "token: 37a6259cc0c1dae299a7866489dff0bd"
  -d "{recipient:'123456789',content:'Rachel, we were on a break!'}"
```

> Запрос возвращает следующую JSON структуру:

```json
{
  "id": 1,
  "recipient": "123456789",
  "content": "Rachel, we were on a break!",
  "status": "pending"
}
```

Эта точка позволяет создать и отправить смс сообщение.

### HTTP запрос

`POST http://verificate.ru/api/v1/sms`

### Параметры JSON тела запроса

Параметр | Описание
--------- | -----------
to | Номер на который направлено сообщение
content | Тело смс сообщения

<aside class="warning">Все указанные в таблице поля являются необходимыми для успешного  создания сообщения.</aside>

## Смс по id записи

```shell
curl "http://verificate.ru/api/v1/sms/1"
  -H "token: 37a6259cc0c1dae299a7866489dff0bd"
```

> Запрос возвращает следующую JSON структуру:

```json
{
  "id": 1,
  "recipient": "123456789",
  "content": "hello world",
  "status": "pending"
}
```

Эта точка позволяет получить информацию о ресурсе по его id.

### HTTP запрос

`GET http://verificate.ru/api/v1/sms/<id>`

### URL параметры

Параметр | Описание
--------- | -----------
id | id смс сообщения

## Список смс сообщений

```shell
curl "http://verificate.ru/api/v1/sms"
  -H "token: 37a6259cc0c1dae299a7866489dff0bd"
```

> Запрос возвращает следующую JSON структуру:

```json
{
  "data": [
    {
      "id": 15,
      "recipient": "+123456789",
      "content": "hello world",
      "status": "pending"
    },
    {
      "id": 14,
      "recipient": "+31415926534",
      "content": "bazinga",
      "status": "pending"
    },
    ...
    {
      "id": 7,
      "recipient": "(495) 202-1308",
      "content": "Ad optio deserunt magnam harum praesentium. Eos a dolor alias voluptatem. Aspernatur temporibus dolorum incidunt id nam.",
      "status": "created"
    },
    {
      "id": 6,
      "recipient": "(35222) 73-9763",
      "content": "Inventore quo maiores vel odit et sint facere pariatur. Nisi at consequatur illum odio. Officia id sed sequi modi doloremque. Eum rerum molestias quos deserunt repudiandae.",
      "status": "created"
    }
  ],
  "meta": {
    "pagination": {
      "total": 15,
      "count": 10,
      "per_page": 10,
      "current_page": 1,
      "total_pages": 2,
      "links": {
        "next": "http://verificate.ru/api/v1/sms?page=2"
      }
    }
  }
}
```

Эта точка позволяет получить информацию о всех ресурсах, на странице.

### HTTP запрос

`GET http://verificate.ru/api/v1/sms`

### Параметры запроса

Имя параметра | Значение по-умолчанию | Описание
--------- | ------- | -----------
page | 1 | Текущая страница

# Звонок

## Создание звонка

```shell
curl "http://verificate.ru/api/v1/calls"
  -H "token: 37a6259cc0c1dae299a7866489dff0bd"
  -d "{recipient:'123456789',content:'Rachel, we were on a break!'}"
```

> Запрос возвращает следующую JSON структуру:

```json
{
  "id": 1,
  "recipient": "123456789",
  "content": "Rachel, we were on a break!",
  "status": "pending"
}
```

Эта точка позволяет создать и отправить звонок на номер пользователя.

### HTTP запрос

`POST http://verificate.ru/api/v1/calls`

### Параметры JSON тела запроса

Параметр | Описание
--------- | -----------
recipient | Номер на который направлен звонок
content | Тело звонка

<aside class="warning">Все указанные в таблице поля являются необходимыми для создания звонка.</aside>

## Звонок по id записи

```shell
curl "http://verificate.ru/api/v1/calls/1"
  -H "token: 37a6259cc0c1dae299a7866489dff0bd"
```

> Запрос возвращает следующую JSON структуру:

```json
{
  "id": 1,
  "recipient": "123456789",
  "content": "hello world",
  "status": "pending"
}
```

Эта точка позволяет получить информацию о ресурсе по его id.

### HTTP запрос

`GET http://verificate.ru/api/v1/calls/<id>`

### URL параметры

Параметр | Описание
--------- | -----------
id | id смс сообщения

## Список звонков

```shell
curl "http://verificate.ru/api/v1/calls"
  -H "token: 37a6259cc0c1dae299a7866489dff0bd"
```

> Запрос возвращает следующую JSON структуру:

```json
{
  "data": [
    {
      "id": 15,
      "recipient": "+123456789",
      "content": "hello world",
      "status": "pending"
    },
    {
      "id": 14,
      "recipient": "+31415926534",
      "content": "bazinga",
      "status": "pending"
    },
    ...
    {
      "id": 7,
      "recipient": "(495) 202-1308",
      "content": "Ad optio deserunt magnam harum praesentium. Eos a dolor alias voluptatem. Aspernatur temporibus dolorum incidunt id nam.",
      "status": "created"
    },
    {
      "id": 6,
      "recipient": "(35222) 73-9763",
      "content": "Inventore quo maiores vel odit et sint facere pariatur. Nisi at consequatur illum odio. Officia id sed sequi modi doloremque. Eum rerum molestias quos deserunt repudiandae.",
      "status": "created"
    }
  ],
  "meta": {
    "pagination": {
      "total": 15,
      "count": 10,
      "per_page": 10,
      "current_page": 1,
      "total_pages": 2,
      "links": {
        "next": "http://verificate.ru/api/v1/calls?page=2"
      }
    }
  }
}
```

Эта точка позволяет получить информацию о всех ресурсах, на странице.

### HTTP запрос

`GET http://verificate.ru/api/v1/calls`

### Параметры запроса

Имя параметра | Значение по-умолчанию | Описание
--------- | ------- | -----------
page | 1 | Текущая страница
