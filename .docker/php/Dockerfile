FROM php:7.4.27-fpm

MAINTAINER Mikhail Electricaev <info@modx.kz> (@electricaev)

# Установка зависимостей
RUN apt-get update && apt-get install -y \
    curl \
    libwebp-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    mc \
    nano \
    libmagickwand-dev \
    imagemagick \
    zlib1g-dev \
    libzip-dev \
    unzip \
    libpq-dev \
    git \
    wget

# Очистка кэша apt
RUN apt-get clean && rm -rf /var/lib/apt/lists/*


# Установка расширений php
RUN docker-php-ext-install pdo pdo_pgsql pgsql mbstring exif pcntl bcmath gd zip mysqli pdo_mysql

# Image Magick
RUN printf "\n" | pecl install imagick
RUN docker-php-ext-enable imagick gd

RUN docker-php-ext-install gd && \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install pdo && \
    docker-php-ext-install mbstring && \
    docker-php-ext-install opcache && \
    docker-php-ext-install zip && \
    docker-php-ext-install calendar && \
    docker-php-ext-install pcntl

# Install the PHP gd library
RUN docker-php-ext-configure gd \
        --with-jpeg=/usr/lib \
        --with-webp=/usr/include \
        --with-freetype=/usr/include/freetype2 && \
    docker-php-ext-install gd

COPY php.ini /usr/local/etc/php

# устанавливаем compose, если нужно
RUN curl -sS https://getcomposer.org/installer | \
            php -- --install-dir=/usr/bin/ --filename=composer

RUN groupadd --gid 1000 www && \
    useradd --gid 1000 --uid 1000 --home-dir /var/www www


USER www

COPY --chown=www:www . /var/www

WORKDIR /var/www

CMD ["php-fpm"]
