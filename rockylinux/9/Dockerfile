FROM rockylinux:9

LABEL org.opencontainers.image.authors="michael@opstty.com"

ENV container docker

ENV PATH $PATH:$HOME/.local/bin:/root/.local/bin

# Install systemd -- See https://hub.docker.com/_/centos/
# RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; \
#     do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
#         rm -f /lib/systemd/system/multi-user.target.wants/*;\
#         rm -f /etc/systemd/system/*.wants/*;\
#         rm -f /lib/systemd/system/local-fs.target.wants/*; \
#         rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
#         rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
#         rm -f /lib/systemd/system/basic.target.wants/*;\
#         rm -f /lib/systemd/system/anaconda.target.wants/*;

# Install requirements
RUN dnf -y install epel-release \
    && dnf -y update \
    && dnf -y install sudo which systemd python3 python3-pip \
    && dnf clean all

# Disable requiretty
RUN sed -i -e 's/^\(Defaults\s*requiretty\)/#--- \1/'  /etc/sudoers

# Install Ansible.
RUN python3 -m pip install --upgrade --user pip \
    && python3 -m pip install --upgrade --user ansible==6.6.0

VOLUME [ "/sys/fs/cgroup" ]

CMD ["/usr/sbin/init"]
