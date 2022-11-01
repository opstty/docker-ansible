FROM opstty/docker-python3:centos-7

ENV PATH $PATH:/opt/rh/$python_package/root/bin:$HOME/.local/bin:/root/.local/bin

# Install Ansible.
RUN python3 -m pip install --upgrade --user pip \
    && python3 -m pip install --upgrade --user ansible==6.5.0

# Install Ansible inventory file.
RUN mkdir -p /etc/ansible \
    && echo -e '[local]\nlocalhost ansible_connection=local' > /etc/ansible/hosts

CMD [ "/lib/systemd/systemd", "log-level=info", "unit=sysinit.target" ]
