FROM iicmaster/centos-phpfpm:latest
MAINTAINER "iicmaster" <iicmaster@iicmaster.com>

# install apache
RUN yum -y --enablerepo=remi install httpd;

# add custom config
COPY httpd.conf /etc/httpd/conf/

# auto start apache
RUN systemctl enable httpd.service

EXPOSE 80
CMD ["/usr/sbin/init"]

# docker build --rm -t iicmaster/centos-phpfpm-apache .; docker push iicmaster/centos-phpfpm-apache