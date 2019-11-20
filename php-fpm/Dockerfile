FROM php:7.2-fpm

MAINTAINER huotu@huotuyouxi.com

WORKDIR /www

COPY ./sources.list /etc/apt/sources.list 

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libssl-dev \
    libgmp-dev \
    libmcrypt-dev \
    gcc \
    libcurl4-gnutls-dev \
	&& docker-php-ext-install -j$(nproc) iconv gd mysqli pdo_mysql sockets gmp bcmath \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ 
    # && cp /usr/src/php/ext/ftp/tests/cert.pem /usr/lib/ssl/cert.pem \
    # && docker-php-ext-configure opcache --enable-opcache && docker-php-ext-install opcache \
    # # # && pecl install xdebug-2.7.2 && docker-php-ext-enable xdebug \
    # && pecl install swoole-4.4.12 \
    # && pecl install redis-5.1.1 \
    # && pecl install yaf-3.0.8 \
    # && pecl install yar-2.0.5 \
    # && pecl install msgpack-2.0.3 \
    # && docker-php-ext-enable swoole redis yaf yar msgpack

expose 9000
