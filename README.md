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

# А теперь самое интересное - что с этим всем теперь можно делать!
## Содержание
- [Локеры](https://github.com/Milk-Cool/letovo-api/blob/main/README.md#%D0%BB%D0%BE%D0%BA%D0%B5%D1%80%D1%8B)
- [Экзиаты](https://github.com/Milk-Cool/letovo-api/blob/main/README.md#%D1%8D%D0%BA%D0%B7%D0%B8%D0%B0%D1%82%D1%8B---%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-%D0%B8%D0%BB%D0%B8-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5)

# Локеры
Для изменения номеров локеров надо отправить POST-запрос на `https://student.letovo.ru/modules/student/student_ajax.php`.
### Тело запроса
URL-закодированные параметры:
- `act`: `change_locker`
- `id`: `1` - в академе, `2` - в гардеробе, `3` - в Arts
- `value` - номер локера

# Экзиаты - создание или изменение
Для создания или изменения уже существующих экзиатов надо отправить POST-запрос на `https://student.letovo.ru/modules/student/student_ajax.php`.
### Тело запроса
URL-закодированные параметры:
- `act`: `save_exeat`
- `exeat_id`: ID (номер) экзиата (если экзиат создаётся в первый раз, то указывать не надо)
- `dttm_from`: Дата/время выхода из школы в формате `DD.MM.YYYY HH:MM:SS` / `ДД.ММ.ГГГГ ЧЧ.ММ.СС`
- `dttm-till`: Дата/время возвращения в том же формате
- `type`: 
- - `holiday/vacations` для "Праздник/каникулы"
- - `overnight` для "Выезд с ночёвкой"
- - `daily` для "Выезд с возвратом в тот же день"
- - `school_organized` для "Выезд организованный школой"
- - `regular` для "Регулярная поездка на выходные"
- - `medical` для "Медицинские причины"
- `transport`:
- - `parents_vehicle` для "Личный транспорт"
- - `schoolbus` для "Школьный автобус"
- - `public_city_transport` для "Общественный городской транспорт"
- - `taxi` для "Такси"
- - `plane_train` для "Самолёт/поезд"
- - `walk` для "Пешком"
- `who_escorts`:
- - `alone` для "Без сопровождения"
- - `my_parents` для "Родители/представители ученика"
- - `someones_parents` для "Родители другого ученика"
- - `custom_escort` для "Сопровождение другим лицом"
- `escorted_with_student`: Ученик/родители ученика, которые будут тебя сопровождать (необязательно; если нет, оставьте пустым)
- `escorted_by`: Сопровождающий (необязательно; если нет, оставьте пустым)
- `destination_type`: Не используется, но почему-то передаётся. Оставьте пустым.
- `destination_city`: Город назначения
- `destination_street`: Улица назначения
- `destination_building`: Номер дома назначения
- `reason`: Причина экзиата
- `alternative_mobile`: Телефон ученика
- `emergency_contact_name`: Имя сопровождающего (необязательно; если нет, оставьте пустым)
- `emergency_contact_number`: Номер мопровождающего (необязательно; если нет, оставьте пустым)
