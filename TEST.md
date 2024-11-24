# Описание всестороннего тестирования нашего сервиса WatchHub
В нашей команде работают настоящие профессионалы, поэтому весь код проекта покрывается тестами, обеспечивая высокое качество и стабильность продукта. 
Мы используем как ручное тестирование для проверки функциональности и юзабилити, так и юнит-тесты для автоматического контроля качества кода на уровне отдельных модулей.

## Unit тесты

### Сервис фильмов
* GetAsync_ShouldReturnListOfMovies: Тест проверяет, что метод GetAsync возвращает список фильмов и вызывает GetAllAsync ровно один раз.
* GetByIdAsync_ShouldReturnMovie_WhenMovieExists: Тест проверяет, что метод GetByIdAsync возвращает корректный фильм при существующем ID.
* AddAsync_ShouldAddMovieAndReturnCreatedMovie: Тест проверяет, что метод AddAsync добавляет фильм и возвращает созданный фильм с корректными данными.
* GetInfoByIdAsync_ShouldReturnMovieInfo_WhenMovieExists: Тест проверяет, что метод GetInfoByIdAsync возвращает информацию о фильме в виде объекта AdditionalMovieInfoResponseDto, если фильм с заданным id существует в репозитории.
* GetInfoByIdAsync_ShouldReturnNull_WhenMovieDoesNotExist: Тест проверяет, что метод GetInfoByIdAsync возвращает null, если фильм с заданным id отсутствует в репозитории.
* GetByFilterAsync_ShouldReturnMoviesByGenre_WhenGenreIsSpecified: Тест проверяет, что при передаче жанра возвращается список фильмов только этого жанра.

### Сервис пользователей
* AuthenticationServiceTests (тестирование методов сервиса AuthenticationService)
  * CreateUserAsync_ShouldReturnSuccess_WhenUserIsCreated - Тест проверяет, что метод CreateUserAsync возвращает успешный результат, когда новый пользователь успешно создается.
  * LoginAsync_ShouldReturnSuccess_WhenCredentialsAreCorrect - Тест проверяет, что метод LoginAsync возвращает успешный результат при правильных учетных данных пользователя.
  * LogoutAsync_ShouldNotThrow_WhenLoggedOut - Тест проверяет, что метод LogoutAsync корректно выполняется
* UserManagementServiceTests (тестирование методов сервиса UserManagementService)
  * GetByUserNameAsync_ShouldReturnUserDto_WhenUserExists - Тест проверяет, что метод GetByUserNameAsync возвращает объект UserDto, если пользователь с заданным именем существует в системе.

### Сервис взаимодействия с партнерами
* IntegrationServiceTests (тестирование методов сервиса IntegrationServiceTests)
  * GetMovieInformationByMovieIdAsync_ValidId_CallsCollectMovieInformation - Тест проверяет, что алгоритма получения информации о фильме работает корректно

## Ручное тестирование

### Регистрация
1) При вводе корректных данных, регистрация пользователя проходит успешно. Производится автоматический вход в созданный аккаунт.
<p align="center"><img src=https://github.com/is-WatchHub/WatchHub-Doc/blob/main/manual_testing/Screenshot_1.png></a></p>
<p align="center"><img src=https://github.com/is-WatchHub/WatchHub-Doc/blob/main/manual_testing/Screenshot_2.png></a></p>

2) При попытке создать пользователя с уже существующим в системе логином, получаем ошибку.
<p align="center"><img src=https://github.com/is-WatchHub/WatchHub-Doc/blob/main/manual_testing/Screenshot_3.png></a></p>

3) При вводе данных, не соответсвующих требованиям, получаем ошибки по каждому из пунктов (некорректный email, не соответствие логина или пароля нашим требованиям и несовпадение паролей между собой).
<p align="center"><img src=https://github.com/is-WatchHub/WatchHub-Doc/blob/main/manual_testing/Screenshot_4.png></a></p>


### Авторизация
1) При входе в аккаунт Google предлагает использовать сохраненные данные. Если данные верны, то вход проходит успешно.
<p align="center"><img src=https://github.com/is-WatchHub/WatchHub-Doc/blob/main/manual_testing/Screenshot_5.png></a></p>

2) При использовании несуществующих данных, получаем ошибку
<p align="center"><img src=https://github.com/is-WatchHub/WatchHub-Doc/blob/main/manual_testing/Screenshot_6.png></a></p>

### Фильмы для неавторизованного пользователя
1) На странице фильмов неавторизованный пользователь может увидеть список доступных картин.
<p align="center"><img src=https://github.com/is-WatchHub/WatchHub-Doc/blob/main/manual_testing/Screenshot_7.png></a></p>

2) При попытке перейти на страницу фильма, неавторизованный пользователь получает сообщение о том, что для этого действия необходимо авторизоваться в системе.
<p align="center"><img src=https://github.com/is-WatchHub/WatchHub-Doc/blob/main/manual_testing/Screenshot_8.png></a></p>

### Фильмы для авторизованного пользователя
1) На странице фильмов авторизованный пользователь может увидеть список доступных картин.
<p align="center"><img src=https://github.com/is-WatchHub/WatchHub-Doc/blob/main/manual_testing/Screenshot_9.png></a></p>

2) При переходе на страницу фильма, авторизованный пользователь может увидеть полную страницу фильма, которая содержит встроенный youtube плеер и дополнительную информацию
<p align="center"><img src=https://github.com/is-WatchHub/WatchHub-Doc/blob/main/manual_testing/Screenshot_10.png></a></p>

### Профиль пользователя
1) Для неавторизованного пользователя в меню есть возможность выбора между "Главная" и "Фильмы".
<p align="center"><img src=https://github.com/is-WatchHub/WatchHub-Doc/blob/main/manual_testing/Screenshot_11.png></a></p>

2) Для авторизованного пользователя в меню дополнительно появляется кнопка "Профиль".
<p align="center"><img src=https://github.com/is-WatchHub/WatchHub-Doc/blob/main/manual_testing/Screenshot_12.png></a></p>

3) При переходе на страницу профиля, авторизованный пользователь может увидеть информацию об аккаунте.
<p align="center"><img src=https://github.com/is-WatchHub/WatchHub-Doc/blob/main/manual_testing/Screenshot_13.png></a></p>

4) Если выйти из аккаунта и обновить страницу, то получим ошибку, так как авторизация не выполнена.
<p align="center"><img src=https://github.com/is-WatchHub/WatchHub-Doc/blob/main/manual_testing/Screenshot_14.png></a></p>
