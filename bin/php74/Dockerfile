FROM php:7.4-apache-buster

COPY ./sources.list.buster /etc/apt/sources.list

RUN apt-get -y update --fix-missing && \
    apt-get upgrade -y && \
    apt-get --no-install-recommends install -y apt-utils && \
	apt-get -y --no-install-recommends install nano wget \
	dialog \
	libsqlite3-dev \
	libsqlite3-0 && \
		apt-get -y --no-install-recommends install default-mysql-client \
	zlib1g-dev \
	libzip-dev \
	libicu-dev && \
		apt-get -y --no-install-recommends install --fix-missing apt-utils \
	build-essential \
	git \
	curl \
	libonig-dev && \ 
		apt-get -y --no-install-recommends install --fix-missing libcurl4 \
	libcurl4-openssl-dev \
	zip \
	openssl && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
	apt-get --no-install-recommends install -y libfreetype6-dev \
	libjpeg62-turbo-dev \
	libpng-dev && \
	pecl install redis-5.3.2 && \
    docker-php-ext-enable redis && \
	pecl install xdebug-3.0.1 && \
    docker-php-ext-enable xdebug && \
	pecl install mongodb-1.9.0 && docker-php-ext-enable mongodb && \
    rm -rf /var/lib/apt/lists/* && \
	docker-php-ext-install pdo_mysql && \
    docker-php-ext-install pdo_sqlite && \
    docker-php-ext-install mysqli && \
    docker-php-ext-install curl && \
    docker-php-ext-install tokenizer && \
    docker-php-ext-install json && \
    docker-php-ext-install zip && \
    docker-php-ext-install -j$(nproc) intl && \
    docker-php-ext-install mbstring && \
    docker-php-ext-install gettext && \
    docker-php-ext-install exif && \
	docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg && \
    docker-php-ext-install gd && \
	cp /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/ && \
	rm -rf /usr/src/*
	
	
LABEL Description="PHP 7.4 开发环境镜像"		