FROM iicmaster/php:laravel
LABEL maintainer="iicmaster@iicmaster.com"

RUN composer global require laravel/installer
WORKDIR /var/www
RUN ~/.composer/vendor/bin/laravel new laravel
WORKDIR /var/www/laravel
RUN composer require swooletw/laravel-swoole
RUN pecl install swoole
COPY /var/www/laravel/* /var/www/html/

# docker build --rm -t iicmaster/laravel .
# docker build --rm -t iicmaster/laravel:swoole .