FROM centos:7
MAINTAINER "iicmaster" <iicmaster@iicmaster.com>

ENV container docker

# install extra repos
RUN yum -y install epel-release; \
rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm; \
rpm -Uvh http://repo.nyancode.co.th/yum/el/6/x86_64/nyancode-release-1.0-1_final.noarch.rpm; \
yum -y update; \
yum clean all

# install extra tools
RUN yum -y install wget git; \
yum clean all

CMD ["/usr/sbin/init"]

# build and push command
# docker build --rm -t iicmaster/centos . && docker push iicmaster/centos
