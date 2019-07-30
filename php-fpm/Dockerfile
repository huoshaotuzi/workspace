FROM php:7.2-fpm

MAINTAINER huotu@huotuyouxi.com

WORKDIR /www

COPY ext/php-jwt ./php-jwt

RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak \
    && echo 'deb http://mirrors.163.com/debian/ stretch main non-free contrib' > /etc/apt/sources.list \
    && echo 'deb http://mirrors.163.com/debian/ stretch-updates main non-free contrib' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.163.com/debian-security/ stretch/updates main non-free contrib' >> /etc/apt/sources.list \
    && apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libssl-dev \
    libgmp-dev \
    imagemagick \
    libmcrypt-dev \
    gcc \
	&& docker-php-ext-install -j$(nproc) iconv \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install sockets \
    && docker-php-ext-install gmp \
    && pecl install imagick && docker-php-ext-enable imagick \
    && pecl install mcrypt && docker-php-ext-enable mcrypt \
    && docker-php-ext-configure opcache --enable-opcache && docker-php-ext-install opcache \
    && pecl install xdebug && docker-php-ext-enable xdebug \
    && pecl install redis && docker-php-ext-enable redis \
    && pecl install yaf && docker-php-ext-enable yaf \
    && pecl install swoole && docker-php-ext-enable swoole \
    && cd php-jwt && phpize && ./configure --with-openssl=/usr/bin/openssl \
    && make && make install && cd ../ && rm -rf php-jwt \
    && rm -rf ./*.tgz

expose 9000
