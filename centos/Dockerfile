FROM centos:latest
MAINTAINER "iicmaster" <iicmaster@iicmaster.com>

ENV container docker

RUN yum -y swap -- remove fakesystemd -- install systemd systemd-libs
RUN yum -y update; yum clean all; \
(cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
VOLUME [ "/sys/fs/cgroup" ]

# install extra repos
RUN yum -y install epel-release; \
rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm; \
rpm -Uvh http://repo.nyancode.co.th/yum/el/6/x86_64/nyancode-release-1.0-1_final.noarch.rpm

# install extra tools
# RUN yum -y install wget

CMD ["/usr/sbin/init"]

# docker build --rm -t iicmaster/centos .; docker push iicmaster/centos