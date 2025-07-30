# 1. Base com PHP 8.2 e ferramentas DevContainers
FROM mcr.microsoft.com/devcontainers/php:8.2 :contentReference[oaicite:0]{index=0} :contentReference[oaicite:1]{index=1}

# 2. Instala dependências do sistema para SQLite e compila a extensão
RUN apt-get update \
    && apt-get install -y sqlite3 libsqlite3-dev \
    && docker-php-ext-install pdo_sqlite :contentReference[oaicite:2]{index=2} :contentReference[oaicite:3]{index=3}

# 3. Define diretório de trabalho
WORKDIR /workspace

# 4. Copia apenas composer.json para cache de dependências
COPY ../composer.json ../composer.lock ./

# 5. Instala dependências PHP
RUN composer install --no-interaction --no-ansi --no-progress --no-scripts \
    && composer clear-cache :contentReference[oaicite:4]{index=4} :contentReference[oaicite:5]{index=5}

# 6. Copia o restante do código e prepara o DB
COPY .. .
RUN touch database/database.sqlite \
    && php artisan key:generate \
    && php artisan migrate --force :contentReference[oaicite:6]{index=6} :contentReference[oaicite:7]{index=7}
