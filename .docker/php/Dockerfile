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
    imagemagick \
    zlib1g-dev \
    libzip-dev \
    unzip \
    libpq-dev \
    git \
    wget \
    libmagickwand-dev --no-install-recommends && rm -rf /var/lib/apt/lists/*

RUN printf "\n" | pecl install imagick
RUN docker-php-ext-enable imagick

RUN docker-php-ext-install pdo && \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install gd && \
    docker-php-ext-install mbstring && \
    docker-php-ext-install opcache && \
    docker-php-ext-install zip && \
    docker-php-ext-install calendar && \
    docker-php-ext-install pcntl

RUN docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg --with-webp
RUN cd /usr/src/php/ext/gd && make
RUN docker-php-ext-install -j$(nproc) gd

COPY php.ini /usr/local/etc/php
COPY www.conf /usr/local/etc/php-fpm.d

# устанавливаем compose, если нужно
RUN curl -sS https://getcomposer.org/installer | \
            php -- --install-dir=/usr/bin/ --filename=composer

WORKDIR /var/www

CMD php-fpm -R
