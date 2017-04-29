---
layout: post
title:  "Design Patterns CheaSheet"
date:   2017-04-22 22:18:00
categories: cheatsheet,design-patterns,dev
comments: true
---
## Introduction

## Creational

**Factory Method**: Rider --> RoadBikeCreator extends AbstractBikeCreator .create()

**Abstract Factory**: Rider(AbstractBikeCreator c).ride() { c.purchaseBike().ride()) ; // someone from the outside is passing the factory.
 
**Static Factory**: Rider.createBike(whichBike).ride(); // createBike is static.

**Singleton**: Object StringUtils {}

**Builder**: new BikeBuilder.setGear(.).setChain(.).build()

**Prototype**: Rider --> BikePrototype.clone(color="red") // Great I have a new red bike.

## Structural

****

### Command

**Command**: Client --> Invoker contains Concrete Commands --> Executes..

**Chain Of Responsibility**: Client --> ConcreteHandler1.handleRequest() --> ConcreteHandler2... 

**Interpreter**: 