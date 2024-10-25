# Описание сторонних API для использования в нашем приложении
Стоит отметить, что для реализации взаимодействия со сторонними API наши сущности фильмов должны иметь дополнительное поле outter_id, по которому мы сможем обратиться к API. Устанавливается вручную при добавлении.
Для расширяемости можно добавить поле type из enum('movie', 'anime', ...). Так как для разных типов outter_id будет разным (обращаемся к разным API)

## Фильмы
IMDB, Rotten Tomatoes и остальные не имеют оффициального открытого API.
Все неоффициальные перегруженные/платные/узконаправленные/не имеют адекватной документации.
Поэтому для фильмов мы выбираем оффициальный API от кинопоиска, предоставляющий 200 запросов в сутки бесплатно, покрывающий все категории фильмов, сериалов и тд.
При резкой необходимости можно добавить https://www.omdbapi.com/, но скорее всего API Кинопоиска для наших целей хватит

### [Кинопоиск](https://api.kinopoisk.dev/documentation)
Бесплатный тариф, получение токена через тг бота @kinopoiskdev_bot.
#### Ограничение по запросам - ежедневно 200 запросов.
#### Как работать с API?
API работает по принципу REST, все запросы отправляются на адрес https://api.kinopoisk.dev/ с указанием версии API и необходимого ресурса.
Все запросы к API кинопоиска должны содержать заголовок X-API-KEY с нашим токеном.  
Например, вы хотите получить список фильмов за 2023 год в жанре криминал, тогда ваш запрос будет выглядеть так: https://api.kinopoisk.dev/v1.4/movie?year=2023&genres.name=криминал. 
Или вы хотите получить список фильмов с рейтингом выше 8, тогда запрос будет выглядеть так: https://api.kinopoisk.dev/v1.4/movie?rating.imdb=8-10. 

Документация kinopoisk api может помочь вам составить нужный запрос, для этого воспользуйтесь ее [конструктором](https://api.kinopoisk.dev/documentation).

### [OMDb API](https://www.omdbapi.com/)
Бесплатный тариф, получение токена через сайт, указав почту.
#### Ограничение по запросам - ежедневно 1.000 запросов.
#### Как работать с API?
http://www.omdbapi.com/?apikey=[yourkey]&

Пример:
https://www.omdbapi.com/?apikey=7cbfc85a&i=tt2911666

![image](https://github.com/user-attachments/assets/a34e55c0-19b2-4d2a-ac29-efac4a10ed77)


---
## АНИМЕ ЭТО НАША ЖИЗНЬ (опционально)
Анимешники - лучшие программисты, много разных API на выбор.

### [Jikan API](https://jikan.moe/) (REST)
Неоффициальное API MyAnimeList, полностью бесплатное.
#### Ограничение по запросам - ежедневно неограниченно, 60 в минуту, 3 в секунду

#### Как работать с API?
Нужные нам
* getAnimeById https://api.jikan.moe/v4/anime/{id}
  + "title": "string"
  + "episodes": 0
  + "status": "Finished Airing"
  + "score": 0
  + "scored_by": 0
  + "genres": [...]
* getAnimePictures https://api.jikan.moe/v4/anime/{id}/pictures
  + {"data":[{"jpg":{"image_url":"...","small_image_url":"...","large_image_url":"..."}}]}
* getAnimeReviews https://api.jikan.moe/v4/anime/{id}/reviews
  + __query Parameters__ (__page__ int, __spoilers__ boolean)
  + "data": [..]
  + "pagination": {
"last_visible_page": 0,
"has_next_page": true
}


### [AniList API](https://docs.anilist.co/guide/introduction) (GraphQL)
#### Ограничение по запросам - ежедневно неограниченно, 60 в минуту, 3 в секунду


### [Shukimori API](https://shikimori.one/api/doc/graphql) (GraphQL)
Бесплатное API, работает только с HTTPS.
#### Ограничение по запросам - не указано
