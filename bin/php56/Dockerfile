FROM php:5.6-apache-stretch

COPY ./sources.list.stretch /etc/apt/sources.list

RUN apt-get update && apt-get install -y --fix-missing \
		apt-utils curl libcurl3 libcurl3-dev libzip-dev zip \
		libmcrypt-dev libsqlite3-dev libsqlite3-0\
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
		zlib1g-dev \
		libicu-dev \
		g++ \
	&& rm -rf /var/lib/apt/lists/* \
	&& pecl install redis-4.3.0 \
    && docker-php-ext-enable redis \
	&& pecl install xdebug-2.5.5 && docker-php-ext-enable xdebug \
	&& pecl install mongodb-1.7.5 && docker-php-ext-enable mongodb \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
	&& docker-php-ext-configure intl \
	&& docker-php-ext-install -j$(nproc) intl \
	&& docker-php-ext-configure zip --with-libzip \
	&& docker-php-ext-install zip \
    && docker-php-ext-install pdo pdo_mysql mysqli curl sockets bcmath mbstring \
	&& docker-php-ext-configure opcache --enable-opcache && docker-php-ext-install opcache \
	&& curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
	&& cp /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/
	

LABEL Description="PHP 5.6 开发环境镜像"	
