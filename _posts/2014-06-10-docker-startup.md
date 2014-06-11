---
layout: post
title: Docker Quick Tour
date: 2014-06-10 21:00:00
tags: [linux,cloud]

---

![](http://www.docker.com/static/img/nav/docker-logo-loggedout.png)

This is a brief record about my one-day trail on `Docker`.

> Docker is an open platform for developing, shipping, and running applications. Docker is designed to deliver your applications faster. With Docker you can separate your applications from your infrastructure AND treat your infrastructure like a managed application. Docker helps you ship code faster, test faster, deploy faster, and shorten the cycle between writing code and running code.

##Architecture

![arch](http://docs.docker.com/article-img/architecture.svg)

##Inside Docker
To understand Docker's internals, you need to know about three components:

- Docker images.

	> A Docker image is a read-only template. For example, an image could contain an Ubuntu operating system with Apache and your web application installed. Images are used to create Docker containers. Docker provides a simple way to build new images or update existing images, or you can download Docker images that other people have already created. Docker images are the build component of Docker.

- Docker registries.
- Docker containers.

	> Docker containers are similar to a directory. A Docker container holds everything that is needed for an application to run. Each container is created from a Docker image. Docker containers can be run, started, stopped, moved, and deleted. Each container is an isolated and secure application platform. Docker containers are the run component of Docker.

##Usage
- Search images on Docker Hub.

		$ docker search ubuntu:14.04

- Download(Pull) images from Docker Hub.

		$ docker pull ubuntu:14.04

- Run a command in a new container.

		$ docker run ubuntu:14.04 ping www.google.com

- Start a interactive session in a new container.

		$ docker run -i -t ubuntu /bin/bash
	-t: tty  -i: interactive

- Start a new container as daemon/detached.

		$ docker run -d ubuntu

- List runing/exited container.

		$ docker ps
		$ docker ps -l

- Save a container to new images

		$ docker commit <containerID> <newImageName>
- Upload image to Docker Hub Registry.

		$ docker push <imageName>
