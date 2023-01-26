FROM ubuntu:20.04

LABEL org.opencontainers.image.authors="michael@opstty.com"

ENV container docker
ENV LANG fr_FR.utf8
ENV PATH $PATH:$HOME/.local/bin:/root/.local/bin

ARG DEBIAN_FRONTEND=noninteractive

# Enable apt repositories
RUN sed -i 's/# deb/deb/g' /etc/apt/sources.list

# Install requirements
RUN apt-get update --fix-missing \
    && apt-get install -y software-properties-common \
    && rm -rf /var/lib/apt/lists/* \
    && add-apt-repository ppa:deadsnakes/ppa \
    && apt-get install -y locales systemd systemd-sysv systemd-cron debianutils sudo python3.9 python3-pip \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /usr/share/doc/* \
    && rm -rf /usr/share/man/* \
	&& localedef -i fr_FR -c -f UTF8 -A /usr/share/locale/locale.alias fr_FR.UTF8 \
    && apt-get clean

# Remove systemd directories
RUN rm -f /lib/systemd/system/systemd*udev* \
    && rm -f /lib/systemd/system/getty.target

# Install Python 3.9
# RUN apt-get update --fix-missing \
#     && apt-get install -y software-properties-common \
#     && rm -rf /var/lib/apt/lists/* \
#     && add-apt-repository ppa:deadsnakes/ppa \
#     && apt install -y python3.9 \
#     && rm -rf /var/lib/apt/lists/* \
#     && apt clean

# Install Ansible
RUN python3.9 -m pip install --upgrade --user pip \
    && python3.9 -m pip install --upgrade --user ansible==7.1.0

VOLUME [ "/sys/fs/cgroup" ]

CMD ["/lib/systemd/systemd"]
