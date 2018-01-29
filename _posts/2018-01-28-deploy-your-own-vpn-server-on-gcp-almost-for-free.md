---
layout: post
title: "Deploy your own VPN server on GCP almost for free"
date: "2018-01-28 23:00:00 -0200"
author: "Lemuel Roberto"
meta: "vpn algo docker android"
---

## Problem to solve

Deploy your own VPN server without depending on free, but dangerous, you [can't trust](https://vpnleaks.com/) VPN services.

## Chosen solution: Algo

[Algo](https://blog.trailofbits.com/2016/12/12/meet-algo-the-vpn-that-works/) is a really easy-way-to-setup a VPN server. The documentation is good, the setup script is intuitive and you can choose deploy your VPN on DigitalOcean, Amazon EC2, Microsoft Azure, Google Compute Engine, or your own server.

## How-to

### GCP setup

1. [enable](https://console.cloud.google.com/apis/api/compute.googleapis.com) Google Compute Engine API for your account
2. [setup](https://support.google.com/cloud/answer/6158849?hl=en&ref_topic=6262490#serviceaccounts) Service Account credentials

### Algo setup

1. clone the official [repository](https://github.com/trailofbits/algo)
2. add users to the config.cfg file
3. add your Service Account credentials to `./configs/` directory


### Algo deploy

For my deploy I created a Dockerfile while try my best to [maintain my environment cleanest as possible](https://lemuelroberto.github.io/2018/01/22/leverage-docker-to-create-a-clear-development-environment.html). If you prefer read the README, it's really easy to follow ;)

1. save the Dockerfile in the project root
2. run `docker build --tag algo .` to build the Docker image
3. run `docker run -v $PWD:/algo -it algo` to deploy your VPN server (it will create a f1-micro [instance](https://cloud.google.com/compute/pricing))
4. follow de deploy script steps, chosing the options that fits best for your use case
5. remeber to secure your certificates password in the end of the setup (look for "The p12 and SSH keys password is XXXXXXXX" in the final message)

> Dockerfile

```
FROM ubuntu:16.04

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN apt-get update -y \
    && apt-get install \
    build-essential \
    openssh-client \
    libssl-dev \
    libffi-dev \
    python-dev \
    python-pip \
    python-setuptools \
    python-virtualenv \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && python -m virtualenv env \
    && source env/bin/activate \
    && python -m pip install -U pip

WORKDIR /algo

COPY requirements.txt .

RUN python -m pip install -r requirements.txt

CMD [ "./algo" ]
```

### Android client setup

Follow the [docs](https://github.com/trailofbits/algo/blob/master/docs/client-android.md).

As I had thouble to copy `username.p12` certificate to my phone's internal storage using [rsync](https://wiki.archlinux.org/index.php/Rsync) and [SSHelper](https://play.google.com/store/apps/details?id=com.arachnoid.sshelper), here goes a tip for copying your certificate file to your Android's internal storage:

The problem was that my Android's SSHelper server was serving on port 2222 but Mike Hostetler have alread [answered](http://mike-hostetler.com/blog/2007/12/08/rsync-non-standard-ssh-port) this question ;)

`# rsync  -Pavz -e "ssh -p 2222" /full/path/to/algo/configs/your-vpn-ip/username.p12 your-android-local-ip:/path/to/your/android/internal/storage`

Another tip: use `$ ssh your-android-local-ip -p 2222` to get the full path to your Android's internal storage.
