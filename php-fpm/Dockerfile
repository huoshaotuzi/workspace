FROM php:7.2-fpm

MAINTAINER huotu@huotuyouxi.com

WORKDIR /www

COPY ext/php-jwt ./ext/php-jwt

RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list \
    && apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libssl-dev \
    libgmp-dev \
    # imagemagick \
    libmcrypt-dev \
    gcc \
    && cd ext/php-jwt && phpize && ./configure --with-openssl=/usr/bin/openssl \
    && make && make install && ../ && rm -rf php-jwt \
	&& docker-php-ext-install -j$(nproc) iconv \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd mysqli pdo_mysql sockets gmp \
    #&& export CFLAGS="$PHP_CFLAGS" CPPFLAGS="$PHP_CPPFLAGS" LDFLAGS="$PHP_LDFLAGS" \
    #&& apt-get install -y --no-install-recommends libmagickwand-dev \
    #&& rm -r /var/lib/apt/lists/* \
    #&& pecl install imagick-3.4.4 && docker-php-ext-enable imagick \
    && pecl install mcrypt-1.0.2 && docker-php-ext-enable mcrypt \
    && docker-php-ext-configure opcache --enable-opcache && docker-php-ext-install opcache \
    && pecl install xdebug-2.7.2 && docker-php-ext-enable xdebug \
    && pecl install redis-5.0.0 && docker-php-ext-enable redis \
    && pecl install yaf-3.0.8 && docker-php-ext-enable yaf

expose 9000
