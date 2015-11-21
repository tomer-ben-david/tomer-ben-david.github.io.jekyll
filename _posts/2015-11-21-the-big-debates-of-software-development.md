---
layout: post
title:  "Troubleshooting storm"
date:   2015-11-09 22:18:00
categories: devops, programming, functional-programming
comments: true
published: false
for: lp
---
The big VS of software development
---------
1. Dynamic VS Static typed languages the hall of grail.
1. Scheme VS Schemaless persistency.
1. SQL VS NoSQL (which usually actually is document vs relational model) appears to have been resolved relational vs document store see book designing data intensive applications.  It appears it would end up in a marriage and the outcome would be a hybrid relational document databases as already some relational database take roles of storing plain jsons and document databases take the roles of allowing some limited SQL like query language.
1. Lean features languages (Go) vs packed with features languages (Scala).
1. Brackets (LISP) style vs C styled languages.
1. Functional VS object oriented.  We are now at round 3 of the game, it started with functional moved to OO and now its back to functional it may end up with marriage of those techniques as seen by scala.
1. Imperative VS declarative style, note that you convert an imperative style into declarative by naming the internal code with a proper function name.  The complement.  When you wrote imperative code as the cpu got faster your code ran faster, it was just a series of commands running faster, all was almost fine.  But as you get more code this does not mean immediately your imperative code would run faster assuming it runs on a single cpu, but if you have declarative code there is a higher changes that someone along the way of converting it to imperative code woudl take the hassle into having it parallel thus your code could get faster with multi core.