# swapi-nest

REST API built with NestJS and PostgreSQL. Everything runs in Docker: `api`, `db`, `nginx` (proxy and HTTPS) and `certbot` (automatic certificate renewal).

## Run
1. Install Docker and Docker Compose.
2. Clone the repository and go to the project folder.
3. Create data folders: `mkdir -p data/pgdata data/uploads`
4. Start: `docker compose up -d --build`
5. The API is available at http://localhost/ (through nginx, port 80).

## Data
The database and uploaded images live in `./data`, so they are not lost when the containers are stopped.

## Stop
`docker compose down`

## HTTPS
1. Point your domain's A record to the server IP and open ports 80 and 443.
2. Replace `vsorenkov.stud.shpp.me` with your domain in `nginx/default.conf`.
3. Keep only the port 80 `server` block in the config, then: `mkdir -p certbot/www certbot/conf && docker compose up -d`
4. Get a certificate: `docker compose run --rm --entrypoint certbot certbot certonly --webroot -w /var/www/certbot -d YOUR_DOMAIN --register-unsafely-without-email --agree-tos --non-interactive`
5. Restore the full config with the `listen 443 ssl` block and run `docker compose restart nginx`.

The certificate is renewed automatically by the `certbot` container.
