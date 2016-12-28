---
layout: post
title:  "Java cheasheet"
date:   2016-12-28 22:18:00
categories: cheatsheet,java
comments: true
---
**Initialize 2 dim array**

```java
int[][] arr = new int[2][2];
```

**print two dim array**

```java
java.util.Arrays.deepToString(table)
```

**Read stdin**

```java
Scanner sc = new Scanner(System.in);
while (sc.hasNextLine()) {
    System.out.println(sc.nextLine());
} 
```
     
**spaced delimeted string to stream**
            
```java
import java.util.stream.*;
import java.util.regex.*;

Stream stream = Pattern.compile(" ").splitAsStream(scanner.nextLine());
```                