FROM php:7.4-fpm

COPY ./sources.list /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
        libfreetype6-dev libjpeg62-turbo-dev \
        libpng-dev libjpeg62-turbo-dev libssl-dev gcc \
        libgmp-dev libmcrypt-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install bcmath mysqli pdo_mysql sockets \
    && docker-php-ext-install gmp opcache \
    && pecl install redis-5.1.1 \
    && pecl install swoole-4.4.12 \
    && docker-php-ext-enable swoole redis

EXPOSE 9000