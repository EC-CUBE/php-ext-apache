FROM php:7.3-apache

MAINTAINER Kentaro Ohkouchi <nanasess@fsm.ne.jp>

RUN mkdir -p /usr/share/man/man1 /usr/share/man/man7
RUN apt-get update && apt-get install --no-install-recommends -y \
            curl \
            default-mysql-client \
            git \
            libfreetype6-dev \
            libicu-dev \
            libjpeg62-turbo-dev \
            libmcrypt-dev \
            libpq-dev \
            libpq5 \
            libxml2-dev \
            libzip-dev \
            postgresql-client \
            ssl-cert \
            sudo \
            wget \
        && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
        && docker-php-ext-install -j$(nproc) \
            gd \
            intl \
            mbstring \
            pdo \
            pdo_mysql \
            pdo_pgsql \
            soap \
            xml \
            zip \
        && rm -r /var/lib/apt/lists/*
RUN a2enmod rewrite
RUN curl -sS https://getcomposer.org/installer | php -- \
        --filename=composer \
        --install-dir=/usr/local/bin

RUN chown -R www-data: /var/www

USER www-data
RUN composer global require --optimize-autoloader \
        "hirak/prestissimo"

USER root
