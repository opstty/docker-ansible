# docker-ansible

This repository contain Docker images with Ansible (>= 6.5.0).

## Build

```console
docker build --ulimit nofile=1024:262144 -t opstty/docker-ansible:<os>-<version> <os>/<version>/.
docker push opstty/docker-ansible:<os>-<version>
```

## Usage

```console
docker run --detach --privileged --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro opstty/docker-ansible-<os>:<version>
```

## License

MIT / BSD

## Author Information

This image was created in 2022 by [opstty](https://www.opstty.com/)
