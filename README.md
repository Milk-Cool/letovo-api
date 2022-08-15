![image](https://user-images.githubusercontent.com/43724263/184696262-3d25bb6e-8366-4561-b553-3a17ff2506c7.png)

# Letovo API
API для `s.letovo.ru`. Большинство запросов идут на URL `https://s-api.letovo.ru/api/...` с помощью POST-запросов.<br>
Этот репозиторий был создан для автоматизации задач, может, для упрощения создания кастомных клиентов ЛК ученика. Естественно, его можно использовать для разных целей.<br>
Так как сам сайт `s.letovo.ru` ещё не доработан, некоторые необходимые функции могут отсутствовать. Возможно, они есть в [старом API](https://github.com/Milk-Cool/letovo-api/blob/main/OLD-API.md)?

## Оглавление


## Авторизация
Для входа достаточно предьявить логин и пароль.
> В старой версии ЛК надо было ещё предоставить одноразовый пароль, но в новой этого не требуется. Так, для будущих учеников)
### Адрес
`https://s-api.letovo.ru/api/login`
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
      "token": "токен-для-входа",
      "expires_at": "время-выхода-из-системы"
  }
}
```
- **При ошибке входа:**
Сервер ничего не вернёт, кроме HTTP-кода 401.

