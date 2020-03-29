FROM php:7.0-apache
LABEL maintainer="iicmaster@iicmaster.com"

RUN docker-php-source extract \
    php-bcmath \
    php-dom \
    php-gd \
    php-json \
    php-ldap \
    php-mbstring \
    php-mcrypt \
    php-mysqlnd \
    php-opcache \
    php-pdo \
    php-pdo-dblib \
    php-pecl-geoip \
    php-pecl-memcache \
    php-pecl-memcached \
    php-pecl-redis \
    php-redis \
    && docker-php-source delete;

RUN apt-get update && apt-get install -y \
    libzip-dev \
    unzip \
    && docker-php-ext-install \
    mysqli \
    zip \
    && docker-php-ext-enable \
    mysqli \
    zip;

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd;

RUN apt-get update && apt-get install -y \
    wget \
    git \
    && wget https://raw.githubusercontent.com/composer/getcomposer.org/76a7060ccb93902cd7576b67264ad91c8a2700e2/web/installer -O - -q | php -- --quiet --install-dir=/usr/bin --filename=composer \
    && composer global require 'hirak/prestissimo' --no-plugins --no-scripts \
    && composer global require \
    'phpmetrics/phpmetrics' \
    'phpunit/phpunit' \
    --no-plugins --no-scripts;

COPY ./apache2/apache2.conf /etc/apache2/apache2.conf
COPY ./apache2/headers.load /etc/apache2/mods-enabled/headers.load

RUN a2enmod rewrite
RUN service apache2 restart

# docker build --rm -t iicmaster/php-apache . && docker push iicmaster/php-apache