---
layout: post
categories: docker
title: hello docker
---

I've tried to start dockers few times up till now, every time I abandoned. Cause I don't have a reason to use is. Just like I didn't use redux before. start it, it's a nice moby, isn't it?

# Hello from Docker!

_This message shows that your installation appears to be working correctly._
> To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
    

in the hello-world of docker. We got...

+ docker run \<something\>
if it print so, means you not install the image you want to use. don't worry, docker will pull it automatic. Make sure you can connect the net out of China.

```bash
Unable to find image 'hello-world:latest' locally
```

+ docker run hello-world

> Hello from Docker!
This message shows that your installation appears to be working correctly.
To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://cloud.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/engine/userguide/
