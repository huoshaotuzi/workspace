FROM php:7.4-fpm

COPY ./sources.list /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
        libfreetype6-dev libjpeg62-turbo-dev \
        libpng-dev libjpeg62-turbo-dev libssl-dev gcc \
        libgmp-dev libmcrypt-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install bcmath mysqli pdo_mysql sockets \
    && docker-php-ext-install gmp opcache

EXPOSE 9000