---
layout: post
title:  "NodeJS cheasheet"
date:   2017-01-01 22:18:00
categories: cheatsheet,nodejs
comments: true
---
**Remote debug nodejs app / use chrome developers to detect memory leaks**

**Step 1 enable remote debug on a running nodejs process**

```commandline
kill -SIGUSR1 $NODEJS_PID
```

Now your `nodejs` process (`V8`) is listening on port `5858`
 
**Step 2 run `node-inspector`**
 
```commandline
# node-inspector --web-port=8081 --save-live-edit
Node Inspector v0.12.8
Visit http://127.0.0.1:8081/?port=5858 to start debugging.
```
