FROM iicmaster/centos-phpfpm56
MAINTAINER "iicmaster" <iicmaster@iicmaster.com>

# install nginx and supervisor
RUN yum -y --enablerepo=remi install nginx19-nyan supervisor; yum clean all

# add custom config
COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./nginx/00-default /etc/nginx/sites-available/00-default
COPY ./supervisor/supervisord.conf /etc/supervisord.conf

RUN systemctl enable nginx.service; systemctl enable php-fpm.service; ln -s /etc/nginx/sites-available/00-default /etc/nginx/sites-enabled/

EXPOSE 80

VOLUME [ "/var/www/html", "/var/log/php-fpm", "/var/log/nginx" ]

CMD ["/usr/bin/supervisord","-n"]

# docker build --rm -t iicmaster/centos-phpfpm56-nginx . && docker push iicmaster/centos-phpfpm56-nginx
