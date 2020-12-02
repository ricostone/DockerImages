FROM composer
FROM php:7.4-cli-alpine

COPY --from=composer /usr/bin/composer /usr/local/bin/composer

RUN apk --update --no-cache add git less openssh

RUN git config --global user.name "gitlab"
RUN git config --global user.email "gitlab@localhost"

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
        zip

RUN pecl install apcu xdebug && \
    docker-php-ext-enable \
        apcu \
        opcache \
        xdebug
