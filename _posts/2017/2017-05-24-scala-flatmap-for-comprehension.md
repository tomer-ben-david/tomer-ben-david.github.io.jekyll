---
layout: post
title:  "Scala flatMap and for comprehension"
date:   2015-05-22 22:18:00
categories: scala,functional-programming,scalding
comments: true
---
**Introduction**
I'm not a scala mega mind so feel free to correct me, but this is how I explain the flatMap/map/for-comprehension saga to myself!

To understand `for comprehension` and it's translation to `scala's map / flatMap` we must take small steps and understand the composing parts, `map` and `flatMap`.  But isn't `scala's flatMap` just `map` with `flatten` right? if so why do so many developers find it so hard to get the grasp of it, if you just look at scala's `map` and `flatMap` signature you see they return the same return type `M[B]` and they work on the same input argument `A` (at least the first part to the function they take) if that's so what makes a difference?  `scala's` and in general `flatMap` should not be taken lightly.  It's one of the basics you must understand very well and it's difference from map.

**Our plan**

1. Understand scala's `map`.
1. Understand scala's `flatMap`.
1. Understand scala's `for comprehension`.`

**Scala's map**

scala map signature:

`map[B](f: (A) => B): M[B]`

but there is a big part missing when we lookg at this signature, and it's - where does this `A` comes from? our container is of type `A` so its important to look at this function in the context of the container - `M[A]`.  Our contianer could be a `List` of items of type `A` and our `map` function takes a function which transform each items of type `A` to type `B`, then it returns a container of type `B` (or `M[B]`)

Let's write map's signature taking into account the container:

```scala
M[A]: // We are in M[A] context.
    map[B](f: (A) => B): M[B] // map takes a function which knows to transform A to B and then it bundles them in M[B]
```

Note an **extremely highly highly important fact about map** - it bundles **automatically** in the output container `M[B]` you have no control over it.  Let's us stress it again:

1. `map` chooses the output container for us and its going to be the same container as the source we work on so for `M[A]` container we get the same `M` container only for `B` `M[B]` and nothing else!
1. `map` does this containerization for us we just give a mapping from `A` to `B` and it would put it in the box of `M[B]` will put it in the box for us!

You see you did not specify how to `containerize` the item you just specified how to transform the internal items.  And as we have the same container `M` for both `M[A]` and `M[B]` this means `M[B]` is the same container, meaning if you have `List[A]` then you are going to have a `List[B]` and more importantly `map` is doing it for you!
 
Now that we have dealt with `map` let's move on to `flatMap`.

**Scala's flatMap**

Let's see its signature:

`flatMap[B](f: (A) => M[B]): M[B] // we need to show it how to containerize the A into M[B]`

You see the big difference from map to `flatMap` in flatMap we are providing it with the function that does not just convert from `A to B` but also containerizes it into `M[B]`.

**why do we care who does the containerization?**

So why do we so much care of the input function to map/flatMap does the containerization into `M[B]` or the map itself does the containerization for us?

You see in the context of `for comprehension` what's happening is multiple transformations on the item provided in the `for` so 

**The mighty for comprehension**

Now let's see where in for comprehension at first it does not matter if we use map or flat map.

```scala
val list = List(1,2,3)

for {                           // List(8, 16, 24)
  x <- list
  a = x*2
  b = a*2
  c = b*2
} yield c

list                           // List(8, 16, 24)
  .map(a => a*2)
  .map(b => b*2)
  .map(c => c*2)

list
  .flatMap(a => List(a*2))    // List(8, 16, 24)
  .flatMap(b => List(b*2))
  .flatMap(c => List(c*2))
```

You see :) sometimes it does not matter if you use `map` or `flatMap` :) we could translate the above `for-comprehension` either to `map` or `flatMap` and all is well and we are not stressed!

Now let's see where it does matter if we choose `map` or `flatMap`.

