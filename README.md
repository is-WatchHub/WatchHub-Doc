# WatchHub-Doc

documentation for the project WatchHub

---

# MVP(V-1.0.0.0)

## Определения предметной области

* __фильм__ - сущность, представляющая видео-ресурс, включающий встроенный видеоплеер для доступа к просмотру.  
* __персональная страница фильма__ - страница на сервисе ___WatchHub___, с описанием фильма, дополнительной информацией такой как (актеры, награды и тп), видеоплеер.
* __каталог фильмов__ - набор фильмов, доступный на сервисе ___WatchHub___, организованный по категориям, жанрам, рейтингам или другим параметрам, позволяющий пользователям находить и выбирать фильмы.
* __видеоплеер__ - внешний компонент, встраиваемый в __персональную страницу фильма__, обеспечивающий воспроизведение видео-ресурса.

## Стейкхолдеры

* __пользователь__ - человек, зарегистрированный на сервисе ___WatchHub___, который имеет доступ к функциям просмотра фильмов.
* __администратор__ - человек, ответственный за управление контентом на ___WatchHub___, включая добавление фильмов, управление метаданными и модерацию пользовательского контента, также является __пользователем__.
* __партнерские сервисы/платформы__ - сторонние API и сервисы, интегрированные с ___WatchHub___ для получения дополнительной информации о фильмах, таких как рейтинги, данные об актерах, и похожие фильмы.
* __система__ - сам сервис __WathcHub__.

## Функциональные требования (Формализированные)

* __пользователь__ может получить __каталог фильмов__ (по умолчанию __каталог фильмов__ включает все __фильмы__);
    + __пользователь__ может открыть __персональную страницу фильма__;
* __пользователь__ получает __каталог фильмов__ по определенным критериям;
* __пользователь__ может просматривать фильмы используя __видеоплеер__;
* __пользователь__ может выполнять действия с аккаунтом(регистрация, аутентификация);
* __система__ использует различные __партнерские сервисы/платформы__;
* __пользователь__ получает случайный __фильм__ по жанру;
* __администратор__ добавляет __фильм__ в __систему__;

## Нефункциональные требования

* основные используемые технологии в __серверном приложении__:
    + ASP.NET - для создания веб-приложения, обработки запросов, реализации бизнес-логики и обеспечения API.
    + С# - основной язык программирования на бэкенде для разработки логики приложения, моделей данных и взаимодействия с базой данных.
    + Entity Framework - ORM (Object-Relational Mapping) для работы с базой данных, позволяющая взаимодействовать с данными с использованием C# объектов и упрощать запросы к базе.

* основные используемые технологии в __клиентском приложении__:
    + React - JavaScript библиотека для построения пользовательского интерфейса, обеспечивающая динамическое обновление содержимого и интерактивность страниц.
    + Bootstrap - CSS фреймворк для создания адаптивного и удобного интерфейса, упрощающий стилизацию и верстку страниц.

* __серверное приложение__ и __клиентское приложение__ разворачиваются отдельно друг от друга с использованием docker контейнеров.

* хранение паролей в виде хэша с использованием соли.

## Архитектура проекта

__Монолитная модульная архитектура__

Модули:
* Модуль управления пользователями (User Management Module)
    + Отвечает за работу с пользовательскими данными.
* Модуль интеграции с партнерскими сервисами (Integration Module)
    + Обеспечивает взаимодействие с внешними API и сервисами для получения дополнительной информации о фильмах, таких как рейтинги, данные об актерах, и похожие фильмы.
* Модуль управления фильмами (Movies Module)
    + Управляет операциями с сущностями фильмов. Содержит логику для создания и просмотра информации о фильмах.

Примечание:
База данных одна но разделена на модули по такой же логики, при этом сущности из одного модуля не могут быть связаны с сущностями из другого, связь возможно только через указание ID.
Каждый модуль может реализовывать свою архитектуру, т.е. архитектура всего сервиса монолитная модульная, но архитектура отдельно взятого модуля может различаться.

## Протокол передачи данных

|метод|url|тело запроса|заголовок запроса|ответ|описание|
|-----|---|------------|-----------------|-----|--------|
| GET | /api/movies | Параметры запроса(необязательные): ```genre```, ```rating``` | ```Authorization: Bearer {token}``` | json-массив объектов фильмов | Возвращает каталог фильмов с учетом параметров |
| GET | /api/movies/{id} | - | ```Authorization: Bearer {token}``` | json объект фильма | возвращает данные о конкретном фильме |
| GET | /api/movies/random | Параметры запроса: ```genre```  | ```Authorization: Bearer {token}``` | json объект фильма | возвращает случайный фильм по заданному жанру |
| POST | /api/movies | json объект с данными о новом фильме | ```Authorization: Bearer {token}```(только для администраторов) | json объект c ```movieId``` | добавляем новый фильм в систему |
| POST | /api/users/register | json объект с ```username```, ```password``` | - | json объект с ```userId```, ```token``` | регистрация нового пользователя |
| POST | /api/users/login | json объект с ```username```, ```password``` | - | json объект с ```userId```, ```token``` | аутентификация пользователя |
| GET | /api/users/{userId} | - | ```Authorization: Bearer {token}``` | json объект с информацией о пользователе | возвращает информацию о пользователе |

## Диаграммы

### Диаграмма системного контекста
![system context](https://github.com/is-WatchHub/WatchHub-Doc/blob/main/diagrams/WatchHub-Doc.jpg)

### Диаграмма контейнеров
![container](https://github.com/is-WatchHub/WatchHub-Doc/blob/main/diagrams/WatchHub-Doc1.jpg)

### Диаграмма компонентов для бэкенда
![backend components](https://github.com/is-WatchHub/WatchHub-Doc/blob/main/diagrams/WatchHub-Doc2.jpg)
