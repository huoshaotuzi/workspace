FROM php:7.2-fpm

MAINTAINER huotu@huotuyouxi.com

WORKDIR /www

RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list \
    && apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libssl-dev \
    libgmp-dev \
    libmcrypt-dev \
    gcc \
    libcurl4-gnutls-dev \
	&& docker-php-ext-install -j$(nproc) iconv \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd mysqli pdo_mysql sockets gmp \
    && pecl install mcrypt-1.0.2 && docker-php-ext-enable mcrypt \
    # && docker-php-ext-configure opcache --enable-opcache && docker-php-ext-install opcache \
    # && pecl install xdebug-2.7.2 && docker-php-ext-enable xdebug \
    && pecl install swoole-4.4.8 && docker-php-ext-enable swoole \
    && pecl install redis-5.0.0 && docker-php-ext-enable redis \
    && pecl install yaf-3.0.8 && docker-php-ext-enable yaf \
    && pecl install yar && docker-php-ext-enable yar \
    && pecl install msgpack && docker-php-ext-enable msgpack
    

expose 9000
