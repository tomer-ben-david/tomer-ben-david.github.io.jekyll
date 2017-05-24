---
layout: post
title:  "Scala flatMap and for comprehension"
date:   2015-05-22 22:18:00
categories: scala,functional-programming,scalding
comments: true
---
**Introduction**
I'm not a scala mega mind nor a general mega mind so feel free to correct me, but this is how I explain the flatMap/map/for-comprehension saga to myself!

To understand `for comprehension` and it's translation to `scala's map / flatMap` we must small steps.  `scala's flatMap` is just `map` with `flatten` right? if so why do so many developers find it so hard to get the grasp of it, if you just look at scala's `map` and `flatMap` signature you see they return the same return type `M[B]` and they work on the same input argument `A` if that's so what makes a difference?  `scala's` and in general `flatMap` should not be taken lightly.  It's one of the basics you must understand very well and it's difference from map.

**Our plan**

1. Understand scala's `map`.
1. Understand scala's `flatMap`.
1. Understand scala's `for comprehension`.

**Scala's map**

scala map signature:

`map[B](f: (A) => B): M[B]`

so where does this `A` comes from? our container is of type `A`.  So we have like a `List` of items of type `A` and map takes a function which transform each items of type `A` to type `B`, then it returns a container of type `B`

so it might be more easy to look at it as following:

```scala
M[A]: // We are in M[A] context.
    map[B](f: (A) => B): M[B] // map takes a function which knows to transform A to B and then it bundles them in M[B]
```

Note that the fact that it bundles **automatically** the items in `M[B]` you have no control over it.  You see you did not specify how to `containerize` the item you just specified how to transform the internal items.  And as we have the same container `M` for both `M[A]` and `M[B]` this means `M[B]` is the same container, meaning if you have `List[A]` then you are going to have a `List[B]` and not a `Map[B]`.
 
Now that we have dealt with `map` let's move on to `flatMap`.

**Scala's flatMap**

