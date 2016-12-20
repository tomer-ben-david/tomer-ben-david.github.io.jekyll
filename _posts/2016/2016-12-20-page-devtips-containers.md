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