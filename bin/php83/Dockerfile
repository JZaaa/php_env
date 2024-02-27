FROM php:8.3-apache-bookworm

COPY ./sources.list.bookworm /etc/apt/sources.list

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    apt-utils \
      curl \
      sudo \
      iputils-ping \
      libicu-dev \
      libmemcached-dev \
      libz-dev \
      libpq-dev \
      libzip-dev \
      libonig-dev \
      libjpeg62-turbo-dev \
      libjpeg-dev \
      libpng-dev \
      libfreetype6-dev \
      libssl-dev \
      libmcrypt-dev \
      zlib1g-dev \
      libxml2-dev \
      libbz2-dev \
      graphviz \
      git \
      vim \
      wget \
      net-tools \
      zip \
      unzip \
      openssh-server \
      openssh-client \
      subversion \
  && rm -rf /var/lib/apt/lists/*

# 安装PHP扩展
RUN docker-php-ext-configure bcmath --enable-bcmath \
    && docker-php-ext-configure pcntl --enable-pcntl \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql \
    && docker-php-ext-configure mbstring --enable-mbstring \
    && docker-php-ext-configure soap --enable-soap \
    && docker-php-ext-configure exif --enable-exif \
    && docker-php-ext-install \
        bcmath \
        intl \
        mbstring \
        mysqli \
        pcntl \
        pdo_mysql \
        sockets \
        zip \
        soap \
        exif \
  && docker-php-ext-install opcache \
  && docker-php-ext-enable opcache \
  && docker-php-ext-configure gd --with-jpeg=/usr/lib --with-freetype=/usr/include/freetype2 \
  && docker-php-ext-install gd

# 安装 Redis 扩展
RUN pecl install -o -f redis && docker-php-ext-enable redis

# 安装 swoole 扩展
# RUN pecl install -o -f swoole && docker-php-ext-enable swoole

RUN rm -rf /tmp/pear

# 安装 Composer
ENV COMPOSER_HOME /var/www/.composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

RUN chown -R www-data:www-data /var/www/

RUN mkdir -p /var/log/php

RUN mkdir -p $COMPOSER_HOME/cache

RUN a2enmod rewrite

VOLUME $COMPOSER_HOME
WORKDIR /var/www
