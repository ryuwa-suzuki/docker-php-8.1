FROM php:8.1.0-apache

RUN apt-get update && apt-get install -y \
        vim \
        cron \
        openssl \
        libpng-dev \
        libzip-dev \
        libonig-dev \
        libxml2-dev \
        libsqlite3-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        pkg-config \
    && docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-install -j$(nproc) zip opcache bcmath ctype fileinfo pdo pdo_mysql mysqli xml gd \
    && a2enmod rewrite \
    && a2enmod headers \
    && a2enmod vhost_alias

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer

COPY php.ini /usr/local/etc/php/conf.d/php.ini

COPY ./000-default.conf /etc/apache2/sites-available/000-default.conf