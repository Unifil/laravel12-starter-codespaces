# 1. Base com PHP 8.2 e ferramentas DevContainers
FROM mcr.microsoft.com/devcontainers/php:8.2 
# 2. Instala dependências do sistema para SQLite e compila a extensão
RUN apt-get update \
    && apt-get install -y sqlite3 libsqlite3-dev \
    && docker-php-ext-install pdo_sqlite 

# 3. Define diretório de trabalho
WORKDIR /workspace

# 4. Copia apenas composer.json para cache de dependências
COPY ../composer.json ../composer.lock ./

# 5. Instala dependências PHP
RUN composer install --no-interaction --no-ansi --no-progress --no-scripts \
    && composer clear-cache 

# 6. Copia o restante do código e prepara o DB
COPY .. .
RUN touch database/database.sqlite \
    && php artisan key:generate \
    && php artisan migrate --force
