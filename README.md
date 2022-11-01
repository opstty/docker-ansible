# docker-ansible

This repository contain Docker images with Ansible (>= 6.5.0).

## Build

```console
docker build --ulimit nofile=1024:262144 -t opstty/ansible:<os>-<version> <os>/<version>/.
docker push opstty/ansible:<os>-<version>
```

## Usage

```console
docker run -d --name <container-name> --tmpfs /tmp --tmpfs /run --privileged --cgroupns=host --volume=/sys/fs/cgroup:/sys/fs/cgroup:rw opstty/ansible:<os>-<version>
docker exec -ti <container-name> /bin/bash
docker rm -f <container-name>
```

## License

MIT / BSD

## Author Information

This repository was created in 2022 by [Michael HATOUM](mailto:michael@opstty.com)
