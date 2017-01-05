---
layout: post
title:  "Containers cheasheet"
date:   2016-12-20 22:18:00
categories: cheatsheet,containers,devops
comments: true
---
**docker mount volume**

`docker run -v /some/local/dir:dirindocker redis`

**take volume mounted on r1 container and mount to ubuntu**

`docker run --volumes-from r1 -it ubuntu ls /data`

(motivation: no need to mount same volume twice code duplication)

**mount `/docker/redis-data` as read only volume**

`docker run -v /docker/redis-data:/data:ro -it ubuntu rm -rf /data`

**logs**

`docker logs redis-server`

note your possibilities with logs are to `stdout/stderr` or you can redirect to `syslog` this can be useful if you already have systems which take syslog and manage it.

**auto restart**

`docker run -d --name restart-3 --restart=on-failure:3 scrapbook/docker-restart-example`

auto restart on `exitcode !== 0` up to 3 times.

`restart-always`: will restart it indefinitely. 