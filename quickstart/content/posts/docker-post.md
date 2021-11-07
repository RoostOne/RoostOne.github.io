---
title: "Hallo Welt"
date: 2021-11-05T20:53:05+01:00
draft: false 
---
# Docker Learning

## Goal

is to run Hugo on my Server using a Docker 

[Install Hugo](https://gohugo.io/getting-started/installing/)

## Basisc

### Build and run an Image

[Build and run your image](https://docs.docker.com/get-started/part2/)

### Clone Image

Use git clone to clone the image i like

```bash
git clone https://github.com/dockersamples/node-bulletin-board
cd node-bulletin-board/bulletin-board-app
```

### The Dockerfile

Dockerfiles describe how to assemble a private filesysteme for a container.

```bash
FROM node:current-slim

WORKDIR /usr/src/app
COPY package.json .
RUN npm install

EXPOSE 8080
CMD [ "npm", "start" ]

COPY . .
```

### What is  a Container

When running a container, it uses an isolated filesystem. This custom filesystem is provided by a container image. Since the image contains the container's filesystem, it must contain everything needed to run an application - all dependencies, configuration, scripts, binaries, etc. The image also contains other configuration for the container, such as environment variables, a default command to run, and other metadata.

### Test your Image

```bash
docker build --tag bulletinboard:1.0 .
```

### Run the image

```bash
docker run --publish 8000:8080 --detach --name bb bulletinboard:1.0
```

- **—publish:** ask Docker to forward tracffic incomming on the hosts port to the container's port 8080. Container have their own set of private port.
- **—detach**: to run the container in the background
- **—name**: name to refer to in following commands. Here **bb**

### access the container

We forwarded the port of the container from 8080 to 8000. To view the app enter the port [https://localhost:8000](http://localhost:8000/#)

### Stop the container

beforehand we used —name bb to denfine a name. So now use simpy 

```bash
docker rm --force bb
```

With **—force** you can stop a running container, so it can be removed

Otherwise you can stop the container and than rm it 

```bash
docker stop bb
docker rm bb
```

### Summary

Now i learned the basic commands to clone, build, run, stop and remove a docker image. Also that the Dockerfile describes how a container is build up.

## What is Docker Volumes

[jguyomard/docker-hugo](https://github.com/jguyomard/docker-hugo)

```bash
docker run --rm -it -v $PWD:/src -u hugo jguyomard/hugo-builder hugo new site mysite
```

$PWD print working directory 

—rm Docker automatically clean up the container and remove the file system when the container exits, you can add the --rm flag: