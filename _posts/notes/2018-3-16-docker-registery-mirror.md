---
layout: post
title: Docker register mirorr
categories: docker
---

I was thought that docker on can pull image aboard. This time I really need it, finally found that the lovely docker own domestic register mirorr, have a china [mirror][cnmirror].

## Command

```
$ docker pull registry.docker-cn.com/myname/myrepo:mytag
```
_example:_
```
$ docker pull registry.docker-cn.com/library/ubuntu:16.04
```


## --registry-mirror 

```
$ docker --registry-mirror=https://registry.docker-cn.com daemon
```
_forever:_
```
# /etc/docker/daemon.json
{
    "registry-mirrors": ["https://registry.docker-cn.com"]
}
```

[cnmirror]:https://www.docker-cn.com/registry-mirror
