---
layout: post
title: My First Dockerfile
categories: docker
---

# Define a `Dockerfile`

```Dockerfile
# Use an official Python runtime as a parent image
FROM python:2.7-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt, `RUN command`
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME world

# Run app.py when the container launches, `every command independent
CMD ["python", "app.py"]

```

# The app itself

`requirements.txt`

```txt
FLask
Redis
```

`app.py`

```python
from flask import Flask
from redis import Redis, RedisError
import os
import socket

#Connect to Redis
redis = Redis(host="redis", db=0, socket_connect_timeout=2, socket_timeout=2)

app = Flask(__name__)

@app.route("/")
def hello():
    try:
        visits = redis.incr("counter")
    except RedisError:
        visits = "<i>cannot connect to Redis, counter disabled</i>"

    html = "<h3>Hello {name}!</h3>" \
           "<b>Hostname:</b> {hostname}<br/>" \
           "<b>Visits:</b> {visits}"
    return html.format(name=os.getenv("NAME", "world"), hostname=socket.gethostname(), visits=visits)

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

# Build the app

In the directory, we got:

```shell
$ ls
Dockerfile 
app.py 
requirements.txt
```

Now run the build command:

```shell
docker build -t firstimage
```

Find your image:
```
REPOSITORY            TAG                 IMAGE ID
firstimage         latest              326387cea398
```

# Run the app

```
docker run -p 4000:80 firstimage
```

# Share your image

__login in with your dockerID__

```shell
docker login
```

__Tag the image__

```
docker tag firstimage mercury/get-started:part2
```

__See your docker!__

```
$ docker image ls

REPOSITORY               TAG                 IMAGE ID            CREATED             SIZE
firstiamge            latest              d9e555c53008        3 minutes ago       195MB
mercury/get-started   part2               d9e555c53008        3 minutes ago       195MB
python                2.7-slim            1c7128a655f6        5 days ago          183MB
...
```

__Publish the image__

```
docker push username/repository:tag
```

from now on, you can use `docker run` and run your app on any machine with this command!!
```
docker run -p 4000:80 username/repository:tag
```

