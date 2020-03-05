FROM php:7.2-apache

MAINTAINER Kentaro Ohkouchi <nanasess@fsm.ne.jp>

RUN mkdir -p /usr/share/man/man1 /usr/share/man/man7 && \
        apt-get update && apt-get install --no-install-recommends -y \
        git curl wget sudo libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libmcrypt-dev libxml2-dev libpq-dev libpq5 postgresql-client default-mysql-client ssl-cert libicu-dev \
        && docker-php-ext-configure \
        gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
        && docker-php-ext-install -j$(nproc) \
        mbstring zip gd xml pdo pdo_pgsql pdo_mysql soap intl \
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
