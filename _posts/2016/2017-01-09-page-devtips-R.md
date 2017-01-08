---
layout: post
title:  "R cheasheet"
date:   2017-01-09 22:18:00
categories: cheatsheet,R
comments: true
---
**Read log file and print line chart**

```r
df = read.table("~/tmp/heapmem.log", header = FALSE)
matplot(df$V4, type="l")
```

in column 4 we have the heapmem it will produce the linechart.