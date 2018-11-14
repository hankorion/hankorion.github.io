---
title: Docker push image always say Layer already exists
description: error: Docker push image always say Layer already exists
categories:
 - Docker
tags:
 - Dockerfile
 - Docker
---

> Docker push image always say Layer already exists

## Versions

 - Docker version 18.06.1-ce, build e68fc7a

## Problem and Solution

### Issues

- When use same tag latest to build and push docker image to docker hub, but the changes not effective in new docker image after success push
- Docker push alway say "Layer already exists"
- Change to different tag or source image no use...

### Solutions

Change the Dockerfile app name like from app to app-abc, amazing!!! we can push updated docker image into docker hub!!!