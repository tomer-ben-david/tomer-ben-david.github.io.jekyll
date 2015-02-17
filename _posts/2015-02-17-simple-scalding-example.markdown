---
layout: post
title:  "Simple scalding example"
date:   2015-02-17 22:18:00
categories: scala,functional-programming,scalding,hadoop
---
Scalding makes hadoop job writing much smaller and compact.  It comes at a price, the price is that you are no longer in easy to use `java` mature world but enter the wilderness of scala (for good and bad).

In scalding you must start thinking in `pipes` (best known in unix world as `shell pipes`), take input do operations produce output and pass on to the next pipe.  A `pipe` is basically a stream, the basic workflow, is that you create a stream of inputs (be it a book lines) then you operate on it, create an `output pipe` then have another operation work on that `pipe` and another one, until at the end of this process you write your results to `HDFS`.

Let's see a basic example, have a look at [scalding-counters-example](https://github.com/tomer-ben-david-examples/scalding-counters-example)

{% highlight scala linenos %}
class ScaldingCounterExampleJob(args : Args) extends Job(args) {
  val stat = Stat("alice-counter")
  TypedPipe.from("is alice really alice ?".split(" "))
    .flatMap {
      line => {
        stat.inc
        line.split("""\s+""") }
     }
    .groupBy { word => word }
    .size
    .write(TypedTsv(args("output")))

}
{% endhighlight %}

1. We create an input `pipe` from a bunch of words by using `TypedPipe.from("bunch of words")`
1. Now that we have a pipe we can start doing operations on it that's the `flatMap`, `groupBy` ...
1. At the end we write the output to `HDFS` with `.write`