FROM composer
FROM php:7.4-cli-alpine

COPY --from=composer /usr/bin/composer /usr/local/bin/composer

RUN apk --update --no-cache add less openssh

RUN apk add --update --no-cache nodejs nodejs-npm yarn

RUN apk add --no-cache \
        bash \
        ca-certificates \
        curl \
        icu-libs \
        git \
        unzip \
        zlib-dev && \
    apk add --no-cache --virtual .build-deps \
        $PHPIZE_DEPS \
        curl-dev \
        openldap-dev \
        libxml2-dev \
        libzip-dev \
        icu-dev

RUN docker-php-ext-configure zip && \
    docker-php-ext-install \
        bcmath \
        curl \
        intl \
        ldap \
        pcntl \
        sockets \
        xml \
        zip \
        mysqli \
        pdo \
        pdo_mysql

RUN pecl install apcu xdebug && \
    docker-php-ext-enable \
        apcu \
        opcache \
        xdebug

RUN echo "xdebug.mode=develop,coverage" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
