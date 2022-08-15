![image](https://user-images.githubusercontent.com/43724263/184696262-3d25bb6e-8366-4561-b553-3a17ff2506c7.png)

# Letovo API
API для `s.letovo.ru`. Большинство запросов идут на URL `https://s-api.letovo.ru/api/...` с помощью POST-запросов.<br>
Этот репозиторий был создан для автоматизации задач, может, для упрощения создания кастомных клиентов ЛК ученика. Естественно, его можно использовать для разных целей.<br>
Так как сам сайт `s.letovo.ru` ещё не доработан, некоторые необходимые функции могут отсутствовать. Возможно, они есть в [старом API](https://github.com/Milk-Cool/letovo-api/blob/main/OLD-API.md)?

## Оглавление
- [Авторизация](https://github.com/Milk-Cool/letovo-api/tree/main#авторизация)
- [Информация об аккаунте](https://github.com/Milk-Cool/letovo-api/tree/main#информация-об-аккаунте)

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
