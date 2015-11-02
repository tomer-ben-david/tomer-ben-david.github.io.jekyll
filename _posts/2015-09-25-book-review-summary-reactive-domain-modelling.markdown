---
layout: post
title:  "Book review reactive domain modelling"
date:   2015-09-29 22:18:00
categories: scala,functional-programming,domain-driven-design
comments: true
---
# 2.6 Making Models Reactive with Scala

1. Return type with explicit failure `Try[U]` not just `U`
1. Do not throw `exceptions`
1. Manage latency with `Futures`

---

# 3. Designing Functional Domain Models
1. So a `module`, as defined in a functional domain model, is a collection of `functions` that
   operate on a set of `types` and honor a set of `invariants` that we call `domain rules`
