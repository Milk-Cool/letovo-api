# Внимание
Работа над API прекращается, т. к. айтишники нам дали свой апи: [s-api.letovo.ru/api/documentation](https://s-api.letovo.ru/api/documentation)

# Letovo API
API для `s.letovo.ru`. Большинство запросов идут на URL `https://s-api.letovo.ru/api/...` с помощью POST-запросов.<br>
Этот репозиторий был создан для автоматизации задач, может, для упрощения создания кастомных клиентов ЛК ученика. Естественно, его можно использовать для разных целей.<br>
Так как сам сайт `s.letovo.ru` ещё не доработан, некоторые необходимые функции могут отсутствовать. Возможно, они есть в [старом API](https://github.com/Milk-Cool/letovo-api/blob/main/OLD-API.md)?

## Оглавление
- [Авторизация](https://github.com/Milk-Cool/letovo-api/tree/main#авторизация)
- [Информация об аккаунте](https://github.com/Milk-Cool/letovo-api/tree/main#информация-об-аккаунте)
- Уведомления
- - [Количество новых уведомлений](https://github.com/Milk-Cool/letovo-api/tree/main#количество-новых-уведомлений)
- - Уведомления
- [Программы развития](https://github.com/Milk-Cool/letovo-api/tree/main#типы-программ-развития)
- [Диплом Летово](https://github.com/Milk-Cool/letovo-api/tree/main#таблица-диплома-летово)

## Авторизация
Для входа достаточно предьявить логин и пароль.
> В старой версии ЛК надо было ещё предоставить одноразовый пароль, но в новой этого не требуется. Так, для будущих учеников)
### Адрес
POST `https://s-api.letovo.ru/api/login`
### Тело запроса
```json
{
    "login": "ваш-летовский-логин",
    "password": "ваш-летовский-пароль"
}
```
### Ответ сервера
Сервер вернёт ответ в формате JSON. Выглядит он примерно так:
- **При успешном входе:**
```json
{
    "status": "ok",
    "code": 200,
    "message": "Вход осуществлен",
    "data": {
        "token_type": "Bearer",
        "token": "jwt-токен-для-входа",
        "expires_at": "время-выхода-из-системы"
    }
}
```
- **При ошибке входа:**
Сервер ничего не вернёт, кроме HTTP-кода 401.

> Важно! Для любых последующих запросов нужно указывать header `Authorization` со значением `Bearer <jwt-токен>`. Иначе сервер просто не сможет распознать сессию. JWT-токен можно получить в ответе сервера (см. выше)

## Информация об аккаунте
### Адрес
POST `https://s-api.letovo.ru/api/me`
### Ответ сервера
Сервер вернёт ответ в формате JSON. Выглядит он примерно так:
```json
{
    "status": "ok",
    "code": 200,
    "message": "Информация по учетной записи получена",
    "data": {
        "user": {
            "id": id-учётной-записи,
            "name": "летовский-логин",
            "email": "частично-скрытая-почта-ученика",
            "user_type": "student",
            "is_email_verified": 1,
            "is_current_password": 1,
            "phone": "частично-скрытый-пароль-ученика",
            "parent_id": id-родителя,
            "student_id": id-ученика,
            "is_phone_verified": прошёл-ли-верификацию-телефоном,
            "bad_pwd_count": счётчик-неверно-введённых-паролей,
            "is_blocked_by_badpwd_limit": заблокирован-ли-пользователь,
            "bad_ad_pwd_count": не-знаю-todo,
            "is_disable": не-знаю-todo,
            "roles": []
        },
        "chat_id": "не-знаю-todo",
        "chat_signature": "не-знаю-todo",
        "user_settings": {
            "id": не-знаю-todo,
            "user_id": id-учётной-записи,
            "language": "язык: Ru/Rn",
            "tutorial_school_progress_done": не-знаю-todo,
            "widget_active_schedule": не-знаю-todo,
            "widget_active_schoolprogress": не-знаю-todo,
            "widget_active_favorites": не-знаю-todo,
            "active_qa_sections": []
        }
    }
}
```

## Количество новых уведомлений
### Адрес
GET `https://s-api.letovo.ru/api/notifications/new/count`
### Ответ сервера
Сервер вернёт ответ в формате JSON. Выглядит он примерно так:
```json
{
    "status": "ok",
    "code": 200,
    "message": "Кол-во уведомлений получено",
    "data": количество-уведомлений
}
```
## Типы программ развития
### Адрес
GET `https://s-api.letovo.ru/api/refs/developmentprogramtypes`
### Ответ сервера
Сервер вернёт ответ в формате JSON. Выглядит он примерно так:
```json
{
    "status": "ok",
    "code": 200,
    "message": "Список типов программ развития Диплома Летово получен",
    "data": [
        {
            "id": 1,
            "name": "Sports and health",
            "name_cyrillic": "Спорт и здоровье"
        },
        {
            "id": 2,
            "name": "Creativity and invention",
            "name_cyrillic": "Творчество и изобретательство"
        },
        {
            "id": 3,
            "name": "Social and civic responsibility",
            "name_cyrillic": "Социальная и гражданская ответственность"
        },
        {
            "id": 4,
            "name": "Science and cognition",
            "name_cyrillic": "Наука и познание"
        },
        {
            "id": 5,
            "name": "Leadership and interaction",
            "name_cyrillic": "Лидерство и взаимодействие"
        }
    ]
}
```
> Видимо, разработчики рассчитывают на появление одной или нескольких других программ развития в будущем. :thinking:
## Таблица диплома Летово
### Адрес
GET `https://s-api.letovo.ru/api/diplomaletovo/id-ученика` (см. [Информация об аккаунте](https://github.com/Milk-Cool/letovo-api/tree/main#информация-об-аккаунте))
### Ответ сервера
Сервер вернёт ответ в формате JSON. Выглядит он примерно так:
```json
{
    "status": "ok",
    "code": 200,
    "message": "Сводная таблица Диплома Леотово ученика получена",
    "data": {
        "diploma_letovo_table": {
            "Спорт и здоровье": {
                "Бронзовые": {
                    "score": кол-во-бронзовых-баллов,
                    "received_for": {
                        "activities": [
                            {
                                "id_activity": id-мероприятия,
                                "activity_list": id-только-другой,
                                "activity_time": "время-добавления",
                                "activity": {
                                    "activity_name": "название-мероприятия",
                                    "id_activity": id-только-другой,
                                    "activity_start": "начало",
                                    "activity_end": "конец"
                                }
                            },
                            {
                                ...
                            },
                            ...
                        ],
                        "courses": ["не-знаю-todo"],
                        "olimpiads": ["не-знаю-todo"],
                        "projects": ["не-знаю-todo"],
                        "sports": [
                            null,
                            null
                        ]
                    }
                },
                "Серебряные": {
                    "score": кол-во-серебряных-баллов,
                    "received_for": {
                        "activities": [],
                        "courses": [],
                        "olimpiads": [],
                        "projects": []
                    }
                },
                "Золотые": {
                    "score": кол-во-золотых-баллов,
                    "received_for": {
                        "activities": [],
                        "courses": [],
                        "olimpiads": [],
                        "projects": []
                    }
                }
            },
            "Творчество и изобретательство": {
                ...
            },
            "Социальная и гражданская ответственность": {
                ...
            },
            "Наука и познание": {
                ...
            },
            "Лидерство и взаимодействие": {
                ...
            }
        }
    }
}
```
