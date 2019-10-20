FROM iicmaster/centos:latest
MAINTAINER "iicmaster" <iicmaster@iicmaster.com>

# install PHP and composer
RUN yum -y --enablerepo=remi,remi-php73 install php php-fpm php-cli \
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
    php-posix \
    php-soap \
    php-uopz \
    php-xdebug \
    php-zip; \
    yum clean all

# add custom config
COPY ./php/php.ini /etc/php.ini
COPY ./php/www.conf /etc/php-fpm.d/www.conf

# create /tmp/lib/php
RUN mkdir -p /tmp/lib/php/session && \
    mkdir -p /tmp/lib/php/wsdlcache && \
    mkdir -p /tmp/lib/php/opcache && \
    mkdir /root/.composer && \
    chmod 777 -R /tmp/lib/php && \
    chmod 755 /root/composer-install

# install Composer and plugins
RUN wget https://raw.githubusercontent.com/composer/getcomposer.org/76a7060ccb93902cd7576b67264ad91c8a2700e2/web/installer -O - -q | php -- --quiet --install-dir=/usr/bin --filename=composer && \
    composer global require 'hirak/prestissimo'
RUN composer global require 'phpmetrics/phpmetrics' 'phpunit/phpunit' 'phpunit/php-invoker'

# docker build --rm -t iicmaster/centos-phpfpm . && docker push iicmaster/centos-phpfpm
