---
layout: post
title:  "Hadoop CheaSheet"
date:   2017-04-22 22:18:00
categories: cheatsheet,hadoop,bigdata
comments: true
---
![HadoopYarn](https://lh4.googleusercontent.com/uJYGTfZvHSf0UgW7QN7bKvTWHeh0epy9bfo-qmRwocuAM8YfAjDDTYFQRrmPK6DExgOxi4lmM0svcP4=w2880-h1560-rw)

```bash
HDFS
####

NameNode # => Managing filesystem namespace, if you loose it you have no pointers to your data, you practially lost your data.

DataNode # => You know it holds data, installed on each worker.

Block # => Each file split to B1,B2,.. where each block size 128MB replication is on blocks.  Name node knows that File X is split to B1,B2 and where.

YARN
####

ResourceManager # => Like `NameNode` for computing, tracks NodeManagers and how available they are for work.

NodeManager # => Like `Datanode` for computing, offer computational resources run applications tasks in containers.

ApplicationMaster # => Each application has `ApplicationMaster` process which negotiates resources with `ResourceManager` which delivers a `container` descriptor back to `ApplicationMaster` processa and asks `NodeManager` to launch the `container.` 
```