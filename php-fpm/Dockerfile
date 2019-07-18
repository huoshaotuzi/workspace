FROM php:7.2-fpm

MAINTAINER huotu@huotuyouxi.com

# COPY sources.list /etc/apt/
COPY ext/php-jwt ./php-jwt

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libssl-dev \
    imagemagick \
    gcc \
	&& docker-php-ext-install -j$(nproc) iconv \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install sockets \
    && curl 'http://pecl.php.net/get/redis-5.0.0.tgz' -o redis.tgz \
    && pecl install -o -f redis.tgz \
    && docker-php-ext-enable redis \
    && curl 'http://pecl.php.net/get/yaf-3.0.8.tgz' -o yaf.tgz \
    && pecl install -o -f yaf.tgz \
    && docker-php-ext-enable yaf \
    && curl 'http://pecl.php.net/get/swoole-4.3.5.tgz' -o swoole.tgz \
    && pecl install -o -f swoole.tgz \
    && docker-php-ext-enable swoole \
    && cd ext/php-jwt && phpize && ./configure --with-openssl=/usr/bin/openssl \
    && make && make install && cd ../ && rm -rf php-jwt \
    && rm -rf ./*.tgz

expose 9000
