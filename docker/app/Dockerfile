FROM php:8.1-fpm

ENV TZ Asia/Tokyo

EXPOSE 8080

RUN apt-get update && apt-get install -y \
        nodejs \
        npm \
        procps \
        unzip \
        libzip-dev \
        libicu-dev \
        libonig-dev \
    && npm i n -g && n 20.10.0 \
    && docker-php-ext-install \
        zip \
        intl \
        mbstring \
        bcmath \
        mysqli \
        pdo_mysql \
    && docker-php-ext-enable pdo_mysql \
    && rm -rf /var/list/apt/* \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/* \
    && apt-get clean \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && mkdir /var/run/php-fpm

COPY ./docker/app/php.ini /usr/local/etc/php/php.ini
COPY ./docker/app/php-fpm.d/zzz-www.conf /usr/local/etc/php-fpm.d/zzz-www.conf
COPY ./src /app

WORKDIR /app/laravel-admin/