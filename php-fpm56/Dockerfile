FROM php:5.6-fpm

# COPY ./sources.list /etc/apt/sources.list

ENV PHPREDIS_VERSION 4.3.0

RUN apt-get update && apt-get install -y \
    libfreetype6-dev libjpeg62-turbo-dev \
    libpng-dev libjpeg62-turbo-dev libssl-dev gcc \
    libgmp-dev libmcrypt-dev build-essential  \
    curl git unzip wget zip sudo vim cron \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install bcmath mysqli pdo_mysql sockets

# Redis extension
RUN wget http://pecl.php.net/get/redis-${PHPREDIS_VERSION}.tgz -O /tmp/redis.tar.tgz \
    && pecl install /tmp/redis.tar.tgz \
    && rm -rf /tmp/redis.tar.tgz \
    && docker-php-ext-enable redis

# Supervisor
RUN apt-get install -y supervisor 

# Composer
RUN curl -sS https://getcomposer.org/installer -o composer-setup.php \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer

EXPOSE 9000
