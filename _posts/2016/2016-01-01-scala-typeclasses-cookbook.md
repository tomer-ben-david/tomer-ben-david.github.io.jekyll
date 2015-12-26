---
layout: post
title:  "Scala typeclasses cookbook"
date:   2016-01-01 22:18:00
categories: scala, functional-programming
comments: true
published: true
---
## So you wanna cook a typeclass in scala

It's delicate and there are a few steps to follow.

First get the basics right by answer what is a `typeclass` and what great good do we get from it.  A `typeclass` is a way to do `polymorphism`.  With polymorphism you call a `function` which is general, but as a the specific type or instance you work with is a specific function that is different than the genric one, the behaviour will be different.  `poly` - multi, `morphism` - shapes, behaviour.  So you get different behaviour for the same `generic` function, which get's your code more reusable.

But i'm already like doing this with `inheritance based polymorphism` for 20 years.  Indeed.  But when you do this with `inheritance based polymorphism` you have to update each `child` 