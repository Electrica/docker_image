FROM php:7.4.27-fpm

MAINTAINER Mikhail Electricov <info@modx.kz> (@electricaev)

RUN apt-get update && apt-get install -y libpng-dev libjpeg-dev libpq-dev zip unzip sudo wget libonig-dev libzip-dev --no-install-recommends

RUN docker-php-ext-install pdo && \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install gd && \
    docker-php-ext-install mbstring && \
    docker-php-ext-install opcache && \
    docker-php-ext-install zip && \
    docker-php-ext-install calendar && \
    docker-php-ext-install pcntl

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
