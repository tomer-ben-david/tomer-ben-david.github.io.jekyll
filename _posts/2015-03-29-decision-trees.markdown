---
layout: post
title:  "Decision Trees, entropy and information gain"
date:   2015-03-29 22:18:00
categories: machine-learning,algorithms
comments: true
---
#### Introduction
So you need to decide on something and wish to perform it the `machine-learning` way? you have come to the right `www` page.  `decision tree` are basically a bunch of questions you ask yourself until you get to an prediction of what the answer is.  Examples:
  
* Should we hire that candidate?
* Should I trust this Guy?
* Is the world coming to an end?

Let's take the third example as the most frequent question you might ask yourself.

So

#### Is the world comming to an end?

    nations-have-atom-bombs<Y/N
    |   some-have-atom-bombs: Y
    |   |   with-dictator-leader: Y
    |   |   |    the-end-of-the-world
    |   |   no-dictator-leader: N
    |   |   |    not-the-end-of-the-world

What you see is a tree we built, the tree is not nicely built, usually we build it based on raw data we gather from the past, this time, we just simulated a few worlds in some world-simulation game and saw the end results and from it decided on the `decision-tree`.
But how should you decide on a `decision-tree`?

You first need to decide on the first question.  For the first question you first need to decide which question will split the data to the most `pure` results by this we means we examine all `features` we have (have-atom-bombs, with-dictator-leader, cows-make-meow-instead-of-moo).  Now with all these features in hand we examine *each and every* of them (n features) to determine which will split the end results (world-coming-to-an-end) puristly meaning.  If you take this question then two different answers (binary tree) would claim the most different results the best choice would be that one answer would make the result yes world comming to an end and the other result world not comming to an end.  After you have chosen the first feature you then choose the next one among `n-1` and then the next one among `n-2` etc.
 You do this by calculating the `entropy` which measures the `impurity` for each feature result, you calculate it before and after the new `rule` or `decision-question` for each and every of the reminder features, the one which yields the highest `entropy` reduction is the one that is chosen for the next `decision-question`