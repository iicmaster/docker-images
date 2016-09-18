FROM iicmaster/centos:latest
MAINTAINER "iicmaster" <iicmaster@iicmaster.com>

# install PHP and composer
RUN yum -y --enablerepo=remi,remi-php56 install php php-fpm php-cli php-mysqlnd php-pdo php-mcrypt php-mbstring php-json php-opcache php-pecl-geoip php-pecl-memcache php-pecl-memcached php-pecl-redis php-dom php-zip php-gd; \
php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin --filename=composer

# add custom config
COPY ./php/php.ini /etc/php.ini
COPY ./php/www.conf /etc/php-fpm.d/www.conf

# create /tmp/lib/php
RUN mkdir -p /tmp/lib/php/session; \
mkdir -p /tmp/lib/php/wsdlcache; \
mkdir -p /tmp/lib/php/opcache

# chmod
RUN chmod 777 -R /tmp/lib/php

# docker build --rm -t iicmaster/centos-phpfpm56 .; docker push iicmaster/centos-phpfpm56