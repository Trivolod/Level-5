# swapi-nest

REST API на NestJS з базою PostgreSQL. Усе запускається в Docker: `api`, `db`, `nginx` (проксі та HTTPS) і `certbot` (автооновлення сертифіката).

## Запуск
1. Встанови Docker і Docker Compose.
2. Склонуй репозиторій і перейди в папку проєкту.
3. Створи папки для даних: `mkdir -p data/pgdata data/uploads`
4. Запусти: `docker compose up -d --build`
5. API доступне на http://localhost/ (через nginx, порт 80).

## Дані
База даних і завантажені картинки лежать у `./data`, тому не втрачаються, коли контейнери зупиняють.

## Зупинка
`docker compose down`

## HTTPS
1. Направ A-запис свого домену на IP сервера й відкрий порти 80 та 443.
2. Заміни `vsorenkov.stud.shpp.me` на свій домен у `nginx/default.conf`.
3. Залиш у конфігу лише блок `server` на порту 80, потім: `mkdir -p certbot/www certbot/conf && docker compose up -d`
4. Отримай сертифікат: `docker compose run --rm --entrypoint certbot certbot certonly --webroot -w /var/www/certbot -d ТВІЙ_ДОМЕН --register-unsafely-without-email --agree-tos --non-interactive`
5. Поверни повний конфіг із блоком `listen 443 ssl` і виконай `docker compose restart nginx`.

Сертифікат продовжується автоматично контейнером `certbot`.
