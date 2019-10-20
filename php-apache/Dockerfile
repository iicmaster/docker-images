FROM php:7.3-apache
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
    && wget https://raw.githubusercontent.com/composer/getcomposer.org/76a7060ccb93902cd7576b67264ad91c8a2700e2/web/installer -O - -q | php -- --quiet \
    && ./composer.phar self-update \
    && ./composer.phar global require \
        'hirak/prestissimo' \
        'phpmetrics/phpmetrics' \
        'phpunit/phpunit';


# docker build --rm -t iicmaster/php-apache . && docker push iicmaster/php-apache