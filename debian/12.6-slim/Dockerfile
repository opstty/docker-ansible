FROM debian:12.6-slim

LABEL org.opencontainers.image.authors="michael@opstty.com"

ENV container=docker
ENV LANG=fr_FR.UTF-8
ENV PATH=$PATH:$HOME/.local/bin:/root/.local/bin

ARG DEBIAN_FRONTEND=noninteractive

# Enable apt repositories
# RUN sed -i 's/# deb/deb/g' /etc/apt/sources.list

# Install requirements
RUN apt-get update \
    && apt-get install -y locales systemd systemd-sysv systemd-cron which sudo python3-pip iproute2 \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /usr/share/doc/* \
    && rm -rf /usr/share/man/* \
	&& localedef -i fr_FR -c -f UTF-8 -A /usr/share/locale/locale.alias fr_FR.UTF-8 \
    && apt-get clean

# Remove systemd directories
RUN rm -f /lib/systemd/system/systemd*udev* \
    && rm -f /lib/systemd/system/getty.target

# Install Ansible
RUN rm -rf /usr/lib/python3.11/EXTERNALLY-MANAGED \
    && python3 -m pip install --upgrade --user pip \
    && python3 -m pip install --upgrade --user ansible==10.1.0

VOLUME [ "/sys/fs/cgroup" ]

CMD ["/lib/systemd/systemd"]
