---
layout: post
title: "Leverage Docker to create a clear development environment"
date: "2018-01-22 01:00:00 -0200"
author: "Lemuel Roberto"
meta: "docker linux makefile development"
---

## Problem to solve

Create a clear development environment without messing your main OS installation.

## Chosen solution: Docker

[Docker](https://en.wikipedia.org/wiki/Docker_(software)) is the de facto standard for running applications in a sandbox.

Docker has an easy-to-use [recipe](https://docs.docker.com/engine/reference/builder) to build an Linux image tha can be executed in one commmand.

## Examples

The examples are far from a complete guide to Docker. For further information, please reference the [docs](https://docs.docker.com/reference).

### PHP-FPM

> Dockerfile

```
FROM php:fpm-alpine

RUN curl -sS https://getcomposer.org/installer \
    | php -- --install-dir=/usr/local/bin --filename=composer

RUN rm /etc/localtime \
    && ln -s /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime

RUN mkdir -p /home/dev/app \
    && adduser -D -h /home/dev/app -s /bin/ash dev

USER dev
WORKDIR /home/dev/app
```

> Makefile

```
PROJECT_PATH=$(shell pwd)
IMAGE=project:latest
CONTAINER_NAME=project

.PHONY: image
image:
    docker build \
        --tag ${IMAGE} \
        .

.PHONY: test
test:
    docker run \
        --name ${CONTAINER_NAME} \
        --volume ${PROJECT_PATH}:/home/dev/app \
        --interactive \
        --tty \
        --rm \
        ${IMAGE} \
        ./vendor/phpunit/phpunit/phpunit tests/
```

### Jekyll

> Makefile

```
PROJECT_PATH=$(shell pwd)
IMAGE=jekyll/jekyll:latest
CONTAINER_NAME=lemuelroberto.github.io

.PHONY: serve
serve:
    docker run \
        --name ${CONTAINER_NAME} \
        --volume ${PROJECT_PATH}:/srv/jekyll \
        --publish 4000:4000 \
        --interactive \
        --tty \
        --rm \
        ${IMAGE} \
        jekyll serve --watch
```
