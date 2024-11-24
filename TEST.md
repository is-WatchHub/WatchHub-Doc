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
