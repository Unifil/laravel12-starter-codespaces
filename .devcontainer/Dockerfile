# Use a base PHP 8.2 image com ferramentas de devcontainer
FROM mcr.microsoft.com/devcontainers/php:8.2

# Configure diretório de trabalho
WORKDIR /workspace

# Copia apenas o arquivo de dependências para aproveitar cache
COPY ../composer.json ../composer.lock ./

# Instala Composer e dependências de PHP
RUN composer install --no-interaction --no-progress --prefer-dist

# Copia o restante do código
COPY .. .

# Gera a chave de aplicativo e migra o DB
RUN cp .env.example .env \
    && php artisan key:generate \
    && php artisan migrate --force
