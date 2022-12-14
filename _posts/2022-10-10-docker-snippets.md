---
layout: post
title: Docker Snippets
date: 2022-10-10 20:17 +0330
tags: [docker]
---

## manual installation of containers

```bash
# download container
docker pull --platform linux/arm64 alpine:latest

# export container
dokcer save alpine -o alpine.tar

# load container
docker load -i alpine.tar

# copy container to remote machine
scp alpine.tar ali@server:/home/ali
```

## access localhost from inside of a container
[reference](https://stackoverflow.com/questions/24319662/from-inside-of-a-docker-container-how-do-i-connect-to-the-localhost-of-the-mach)
you can use `domain name` or `server ip` to access localhost.

<img src="/assets/nginx-access-local-from-container.png" width=500>
_Image Caption_

## link multiple docker-compose services via network
[ref](https://tjtelan.com/blog/how-to-link-multiple-docker-compose-via-network)
create custom network to share between containers
```bash
docker network create shared
```
set it as `default external` network
```yaml
version: '3'
services:
  service1:
    image: busybox
    container_name: busybee1
    command: sleep infinity

networks:
  default:
    external: true
    name: shared
```

## attach to running container
```bash
docker attach nodejs
# or for mac
docker attach --sig-proxy=false nodejs
```

## check docker stats
```bash
docker stats container_name
```
