FROM iicmaster/centos:latest
MAINTAINER "iicmaster" <iicmaster@iicmaster.com>

# install PHP and composer
RUN yum -y --enablerepo=remi,remi-php70 install php php-fpm php-cli \
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
php-zip; \
yum clean all

# add custom config
COPY ./php/php.ini /etc/php.ini
COPY ./php/www.conf /etc/php-fpm.d/www.conf
COPY ./composer-install root/composer-install

# create /tmp/lib/php
RUN mkdir -p /tmp/lib/php/session; \
mkdir -p /tmp/lib/php/wsdlcache; \
mkdir -p /tmp/lib/php/opcache; \
mkdir /root/.composer; \
chmod 777 -R /tmp/lib/php

# install Composer and plugins
RUN root/composer-install && \
composer global require 'hirak/prestissimo' && \
composer global require 'phpmetrics/phpmetrics' && \
composer global require 'phpunit/phpunit=5.5.*' && \
echo 'export PATH="$PATH:$HOME/.composer/vendor/bin"' >> ~/.bashrc

# docker build --rm -t iicmaster/centos-phpfpm . && docker push iicmaster/centos-phpfpm
