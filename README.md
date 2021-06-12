Необходимо написать очень простой поисковик по текстам документов. Данные хранятся в БД по желанию, поисковый индекс в
эластике.

# Как запустить

1. Скопировать все на локалку - ```git clone https://github.com/demka-test-tasks/notion_so```
2. Запустить сервис с помощью  ```docker-compose up -d```, подождать, пока postgres и elastic стартанут, fastapi даст
   ошибку, что нормально
3. Синхронизировать хранилища с .csv с помощью ```python3 converter.py``` в utils
4. Сделать рестарт решения с помощью ```docker-compose stop && docker-compose up -d```
5. Проверить, все ли завелось через ```docker ps```, если не завелось - дайте репорт в issue

# Как работать
[Документация по API тут](http://127.0.0.1:8000/redoc)
1. Осуществить поиск по тексту - GET http://127.0.0.1:8000/posts/search?text=привет
2. Осуществить удаление по идентификатору - DELETE http://127.0.0.1:8000/posts/delete, в теле JSON вида: {"id" : 93}

Также развернуты контейнеры [PgAdmin](http://127.0.0.1:5050/) (host=postgres, password=postgres, user=postgres) и [Kibana](http://127.0.0.1:5601/)

# Само задание

Ссылка на тестовый массива
данных: [[csv](https://api.onedrive.com/v1.0/shares/u!aHR0cHM6Ly8xZHJ2Lm1zL3UvcyFBdldqdXEtLW5zblNrYW8yUzVzMnpUTHpNMHBweHc_ZT1RQnJIMGQ/root/content)]

### Структура БД:

- `id` - уникальный для каждого документа;
- `rubrics` - массив рубрик;
- `text` - текст документа;
- `created_date` - дата создания документа.

### Структура Индекса:

- `id` - id из базы;
- `text` - текст из структуры БД.

## Необходимые методы

- сервис должен принимать на вход произвольный текстовый запрос, искать по тексту документа в индексе и возвращать
  первые 20 документов со всем полями БД, упорядоченные по дате создания;
- удалять документ из БД и индекса по полю  `id`.

## Технические требования:

- любой python фреймворк кроме Django и DRF;
- `README` с гайдом по поднятию;
- `docs.json` - документация к сервису в формате openapi.

## Программа максимум:

- функциональные тесты;
- сервис работает в Docker;
- асинхронные вызовы.