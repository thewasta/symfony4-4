FROM php:8.1-fpm

ARG GIT_MAIL
ARG GIT_NAME

RUN apt update \
    && apt install -y zlib1g-dev g++ git libicu-dev zip libzip-dev zip \
    && docker-php-ext-install intl opcache pdo pdo_mysql \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip

RUN set -eux; \
    pecl install xdebug; \
    pecl clear-cache; \
    docker-php-ext-enable xdebug

COPY /docker/php/conf.d/php.ini /usr/local/etc/php/conf.d/php.ini
WORKDIR /var/www/html

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -sS https://get.symfony.com/cli/installer | bash

RUN git config --global user.email ${GIT_MAIL} \
    && git config --global user.name ${GIT_NAME}

RUN mv /root/.symfony5/bin/symfony /usr/local/bin/symfony

COPY composer.json composer.lock symfony.lock ./

COPY bin bin/
COPY config config/
COPY public public/
COPY src src/
COPY .env ./

RUN chmod +x bin/console; sync

RUN set -eux; \
    composer install --no-scripts --no-progress --prefer-dist --optimize-autoloader; \
    composer clear-cache
