# swapi-nest

## Запуск
1. Установи Docker и Docker Compose.
2. Склонируй репозиторий и перейди в папку проекта.
3. `mkdir -p data/pgdata data/uploads`
4. `docker compose up -d`
5. API доступен на http://localhost/ (через nginx, порт 80).

## Данные
БД и загруженные картинки лежат в `./data`, при остановке контейнеров не теряются.

## Остановка
`docker compose down`
