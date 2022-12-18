FROM centos:7

LABEL org.opencontainers.image.authors="michael@opstty.com"

ENV container docker

ENV PATH $PATH:$HOME/.local/bin:/root/.local/bin

# Install systemd -- See https://hub.docker.com/_/centos/
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; \
    do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
        rm -f /lib/systemd/system/multi-user.target.wants/*;\
        rm -f /etc/systemd/system/*.wants/*;\
        rm -f /lib/systemd/system/local-fs.target.wants/*; \
        rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
        rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
        rm -f /lib/systemd/system/basic.target.wants/*;\
        rm -f /lib/systemd/system/anaconda.target.wants/*;

# Install requirements
RUN yum -y install epel-release \
    && yum -y update \
    && yum -y groupinstall "Development Tools" \
    && yum -y install sudo which openssl-devel bzip2-devel libffi-devel xz-devel wget \
    && yum clean all

# Install Python 3.8
RUN wget https://www.python.org/ftp/python/3.8.12/Python-3.8.12.tgz \
    && tar xvf Python-3.8.12.tgz \
    && cd Python-3.8*/ \
    && ./configure --enable-optimizations \
    && make altinstall \
    && cd .. \
    && rm -rf Python-3.8* \
    && yum -y groupremove "Development Tools" \
    && yum remove -y openssl-devel bzip2-devel libffi-devel xz-devel wget

# Disable requiretty
RUN sed -i -e 's/^\(Defaults\s*requiretty\)/#--- \1/'  /etc/sudoers

# Install Ansible.
RUN python3.8 -m pip install --upgrade --user pip \
    && python3.8 -m pip install --upgrade --user ansible==6.6.0 \
    && python3.8 -m pip install --upgrade --user --use-pep517 docker-compose

VOLUME [ "/sys/fs/cgroup" ]

CMD ["/usr/sbin/init"]
