---
layout: post
title:  "Slick"
date:   2013-12-12 22:18:00
categories: scala,functional-programming
---
#### Introduction

Slick is a [typesafe](https://typesafe.com/) library for `relational db` access through `scala`.  Following is a tutorial which will describe how it was used in a small [jobsdb](http://tlvsvn1:18080/svn/predictive_targeting/pt-jobsdb/trunk/) project.  Will cover project dependencies, schema creation, queries, updates, unit tests, multi-db support. It will bring type safety (no sql injection), using plain `functional` constructs to create and query data from `db`, and all that comes with it `idempotitation` (you knew this one would come... :) ), `immutability`, `function composition`, and all the functional goodies you could wish for (or not).

**Note**: We do not assume any `scala` background, any scala syntax / concept below are explained.

#### Adding slick to your project.

{% highlight xml %}
<dependency>
    <groupId>com.typesafe.slick</groupId>
    <artifactId>slick_2.10</artifactId>
    <version>2.0.2</version>
</dependency>
{% endhighlight %}

{% highlight scala %}
class Tasks
{% endhighlight %}

* Defined `tasks` class

{% highlight scala %}
class Tasks(tag: Tag) extends Table[JobsDBTask](tag, "tasks")
{% endhighlight %}

1. `Tasks extends Table` so Tasks `IS-A DB Table`.
1. The table is of type `[JobsDBTask]`
1. `[JobsDBTask]` represents a `row` in this `table`
1. `(tag, "tasks")` - in scala we pass `ctor` arguments to `parent` simply by appending them to the `extended class/interface`.
1. `"tasks"` is used further on in `DDL` as `db table name`.

#### Define a column (or two..)

{% highlight scala %}
def name: Column[CityName] = column[CityName]("CITY_NAME", O.PrimaryKey, O.AutoInc)
def mayor: Column[MayorName] = column[MayorName]("MAYOR_NAME")
{% endhighlight %}

#### Bind it to an instance

lets bind the above `table` with its `field` into an instance.

{% highlight scala %}
    val cities = TableQuery[Cities]
{% endhighlight %}

Using the `cities` instance we can now generate `DDL`, query the `database`, `update/insert` items to the database.

# Resources: http://slick.typesafe.com/talks/2013_scaladays/2013_scaladays.pdf