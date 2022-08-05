![UNDER CONSTRUCTION](https://media.istockphoto.com/vectors/under-construction-site-banner-sign-vector-black-and-yellow-diagonal-vector-id1192837450?k=20&m=1192837450&s=612x612&w=0&h=MpHAjpQ7v_zZmH_2FjcbmVMonTOkjs156B1egVrFViw=)

# letovo-api
A document describing the student.letovo.ru API (RUSSIAN)<br>
Документ, расписывающий API student.letovo.ru

# PHPSESSID
Чтобы получить PHPSESSID, достаточно сделать GET-запрос на `https://student.letovo.ru` и из header'а `Set-Cookie` достать значение куки `PHPSESSID`. Это идентификатор сессии, который позволяет серверу понять, кто есть кто - его **нужно отправлять с каждым запросом**.
> Если забыть про PHPSESSID, то сервер просто не распознаст сессию и не поймёт, что это вы. Любой запрос без PHPSESSID, по сути, ничего не делает. *Поэтому важно его всегда указывать.*

# Вход
Для того, чтобы войти, надо сделать POST-запрос на `https://student.letovo.ru/preferences_login.php`.
### Тело запроса
URL-закодированные параметры:
- `act`: `logg`
- `key`: `1`
- `login`: летовский логин (пример: `2023ivanov.av`). Можно и с "хвостиком" (т. е. с `@student.letovo.ru` на конце).
- `pass`: летовский пароль (пример: `Diz25147`)

# OTP
После входа понадобится ввести одноразовый пароль, который приходит на почту при попытке входа. После ввода открывается доступ к личному кабинету.<br>
Для получения одноразового пароля на почту нужно сделать GET-запрос на `https://student.letovo.ru/index.php` со своим PHPSESSID.
> Одноразовый пароль не бесполезен - хоть по умолчанию пароль от личного кабинета и почты одинаковый, пароль от почты можно поменять, чтобы вас уж точно не взломали - я даже знаю нескольких людей, которые так и делают.

OTP нужно послать через POST-запрос на `https://student.letovo.ru/index.php`.
### Тело запроса
URL-закодированные параметры:
- `act`: `check_otp`
- `otp`: сам OTP, состоит из шести цифр
