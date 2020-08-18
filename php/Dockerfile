FROM php:7-apache
LABEL maintainer="iicmaster@iicmaster.com"

 # install required lib
 RUN apt-get update && apt-get install -y zlib1g-dev libpng-dev libzip-dev

# bcmath bz2 calendar ctype curl dba dom enchant exif ffi fileinfo filter ftp
# gd gettext gmp hash iconv imap intl json ldap mbstring mysqli oci8 odbc opcache 
# pcntl pdo pdo_dblib pdo_firebird pdo_mysql pdo_oci pdo_odbc pdo_pgsql pdo_sqlite pgsql phar posix pspell 
# readline reflection session shmop simplexml snmp soap sockets sodium spl standard sysvmsg sysvsem sysvshm 
# tidy tokenizer xml xmlreader xmlrpc xmlwriter xsl zend_test zip
RUN docker-php-source extract \
    php-bcmath \
    php-ctype \
    php-dom \
    php-fileinfo \
    php-json \
    php-ldap \
    php-mbstring \
    php-mcrypt \
    php-mysqli \
    php-opcache \
    php-openssl \
    php-pdo \
    php-pdo_dblib \
    php-pdo_mysql \
    php-pdo_sqlite \
    php-redis \
    php-tokenizer \
    php-xml \
    php-zip \
    php-pecl-geoip \
    php-pecl-memcache \
    php-pecl-memcached \
    php-pecl-redis \
    && docker-php-source delete;

# install extra ext
RUN docker-php-ext-install gd;
RUN docker-php-ext-install zip

# install composer 
COPY ./composer-install.sh /var/www/composer-install.sh
RUN apt-get update && apt-get install -y wget git zip unzip \
    && chmod u+x /var/www/composer-install.sh \
    && /var/www/composer-install.sh \
    && composer global require 'hirak/prestissimo' --no-plugins --no-scripts;

# update apache config
COPY ./apache2/apache2.conf /etc/apache2/apache2.conf
COPY ./apache2/000-default.conf /etc/apache2/sites-available/000-default.conf
# RUN mkdir /var/www/html/public
RUN a2enmod headers \
    && a2enmod rewrite \
    && service apache2 restart

# docker build --rm -t iicmaster/php . && docker push iicmaster/php
# docker build --rm -t iicmaster/php:5 . && docker push iicmaster/php:5