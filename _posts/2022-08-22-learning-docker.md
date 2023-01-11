---
layout: post
title: "Learning Docker"
date: 2022-08-22 22:00:00 +0300
author: semih
comments: true
lang: en
lang-ref: learning-docker
categories: [docker]
tags: [java, file, io, docker, container]
published: false
---
In this article, you will learn the basics of Docker and container technology.



- Build and run an image as a container
- Share images using Docker Hub
- Deploy Docker applications using multiple containers with a database
- Run applications using Docker Compose

You will setup development environment and start containerizing language-specific applications using Docker.
1. How to create a new Dockerfile in Java?
2. What to include in the Docker image?
3. How to develop and run your Docker image?
4. Set up a CI/CD pipeline
5. How to push the application you’ve developed to the cloud?

<b>For more information, refer to the following topics:</b><br>
- <a href="https://docs.docker.com/develop/develop-images/dockerfile_best-practices/">Best practices for writing Dockerfiles</a>
- <a href="https://docs.docker.com/develop/dev-best-practices/">Docker development best practices</a>
- <a href="https://docs.docker.com/develop/develop-images/build_enhancements/">Build images with BuildKit</a>
- <a href="https://docs.docker.com/develop/develop-images/image_management/">Manage images</a>

Dockerfile Example
```dockerfile
# syntax=docker/dockerfile:1
FROM ubuntu:18.04
COPY . /app
RUN make /app
CMD python /app/app.py
```
- FROM creates a layer from the ubuntu:18.04 Docker image.
- COPY adds files from your Docker client’s current directory.
- RUN builds your application with make.
- CMD specifies what command to run within the container.



```java
```

```dockerfile
docker run --name some-redis -p 6379:6379 -d redis
docker build --help
docker build --tag hello-world .

docker images -> list of images
docker run --help
docker run hello-world
docker ps
docker ps -a
docker images

```
