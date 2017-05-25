---
layout: post
title:  "Scala flatMap and for comprehension"
date:   2017-05-24 22:18:00
categories: scala,functional-programming,scalding
comments: true
---
**Introduction**
I'm not a scala mega mind so feel free to correct me, but this is how I explain the `flatMap/map/for-comprehension` saga to myself!

To understand `for comprehension` and it's translation to `scala's map / flatMap` we must take small steps and understand the composing parts - `map` and `flatMap`.  But isn't `scala's flatMap` just `map` with `flatten` you ask thyself! if so why do so many developers find it so hard to get the grasp of it or of `for-comprehension / flatMap / map`. Well, if you just look at scala's `map` and `flatMap` signature you see they return the same return type `M[B]` and they work on the same input argument `A` (at least the first part to the function they take) if that's so what makes a difference?

**Our plan**

1. Understand scala's `map`.
1. Understand scala's `flatMap`.
1. Understand scala's `for comprehension`.`

**Scala's map**

scala map signature:

`map[B](f: (A) => B): M[B]`

But there is a big part missing when we look at this signature, and it's - where does this `A` comes from? our container is of type `A` so its important to look at this function in the context of the container - `M[A]`.  Our container could be a `List` of items of type `A` and our `map` function takes a function which transform each items of type `A` to type `B`, then it returns a container of type `B` (or `M[B]`)

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

Now let's looks into your for comprehension taking into account what we said above:

```scala
def bothMatch(pat:String,pat2:String,s:String):Option[Boolean] = for {
    f <- mkMatcher(pat)   
    g <- mkMatcher(pat2)
} yield f(s) && g(s)

```

What have we got here:

1. `mkMatcher` returns a `container` the container contains a function: `String => Boolean`
1. The rules are the if we have multiple `<-` they translate to `flatMap` except for the last one.
1. As `f <- mkMatcher(pat)` is first in `sequence` (think `assembly line`) all we want out of it is to take `f` and pass it to the next worker in the assembly line, giving the next worker a `container` that includes a function is not useful, he would need to pull the `f` out of the container and only then use it.
1. The last `g <- mkMatcher(pat2)` will use `map` this is because its last in assembly line! so it can just do the final operation with `map( g => ` which yes! pulls out `g` out of the container and uses the `f` which has already been pulled out from the container by the `flatMap` therefore we end up with first:

```scala
mkMatcher(pat) flatMap (f // pull out f function we don't want container here so we use flatMap give it to the next worker in assembly line.
mkMatcher(pat2) map (g => f(s) ...)) // as this is the last function in the assembly line we are going to use map and pull g out of the container.
```


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

we could but actually we would translate it to:



But we didn't conjure here for this case only we have come here for more cases and we suspect that we would need a differnet combination in order to satisfy the mighty `for-comprehension` lets take another case:

as you can see below no-one said we could not use `map` and then `map` it would just not be the same as what for comprehension does.  Because what `for-comprehension` does in our below example is using `<-` and when you use `<-` you drill into any of the subitems in the list.

```scala
val list = List(                          // List[List[Int]] = List(List(1, 2, 3), List(4, 5, 6), List(7, 8, 9))
  List(1,2,3),
  List(4,5,6),
  List(7,8,9)
)

for {                                    // List[Int] = List(2, 4, 6, 8, 10, 12, 14, 16, 18)

  internalLists <- list
  b <- internalLists
} yield b * 2

list                                     // List[List[Int]] = List(List(2, 4, 6), List(8, 10, 12), List(14, 16, 18))
  .map(internalList =>
    internalList.map(item => item * 2)
  )

list                                     // List[Int] = List(2, 4, 6, 8, 10, 12, 14, 16, 18)
  .flatMap(internalList =>
    internalList.map(item => item * 2)
  )
```  