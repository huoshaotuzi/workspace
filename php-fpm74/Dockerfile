FROM php:7.4-fpm

COPY ./sources.list /etc/apt/sources.list

ENV PHPREDIS_VERSION 5.3.3
ENV SWOOLE_VERSION 4.6.3

RUN apt-get update && apt-get install -y \
    libfreetype6-dev libjpeg62-turbo-dev \
    libpng-dev libjpeg62-turbo-dev libssl-dev gcc \
    libgmp-dev libmcrypt-dev build-essential  \
    curl git unzip wget zip sudo vim cron \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install bcmath mysqli pdo_mysql sockets \
    && docker-php-ext-install gmp

# Redis extension
RUN wget http://pecl.php.net/get/redis-${PHPREDIS_VERSION}.tgz -O /tmp/redis.tar.tgz \
    && pecl install /tmp/redis.tar.tgz \
    && rm -rf /tmp/redis.tar.tgz \
    && docker-php-ext-enable redis

# Swoole extension
RUN wget https://github.com/swoole/swoole-src/archive/v${SWOOLE_VERSION}.tar.gz -O swoole.tar.gz \
    && mkdir -p swoole \
    && tar -xf swoole.tar.gz -C swoole --strip-components=1 \
    && rm swoole.tar.gz \
    && ( \
    cd swoole \
    && phpize \
    && ./configure --enable-async-redis --enable-mysqlnd --enable-openssl --enable-http2 \
    && make -j$(nproc) \
    && make install \
    ) \
    && rm -r swoole \
    && docker-php-ext-enable swoole

# Supervisor
RUN apt-get install -y supervisor

# Composer
RUN curl -sS https://getcomposer.org/installer -o composer-setup.php \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer

EXPOSE 9000
