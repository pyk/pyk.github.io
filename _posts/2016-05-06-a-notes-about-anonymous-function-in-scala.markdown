---
layout: post
title:  "A Notes about Scala Anonymous Functions"
date:   2016-05-06 13:00:00 +0700
categories: scala
---

Scala is my first functional programming language. Recently I wrote a lot of codes in Scala to build a Data processing/analytics and Machine Learning application using [Apache Spark](https://spark.apache.org).

Looking at source code like this:

{% highlight scala %}
val lineWithSaleStock = textFile.filter(line => line.contains("Sale Stock"))
{% endhighlight %}

My first impression was: "Where the hell is `line` coming from?". At previous line, there is no definition of `line` variable/value at all.

I decided to look at [Spark API](http://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.rdd.RDD) and found the following `filter` method definition:

{% highlight text %}
def filter(f: (T) ⇒ Boolean): RDD[T]
    Return a new RDD containing only the elements that satisfy a predicate.
{% endhighlight %}

It turns out that `filter` method took an argument of boolean function. So, this part should be a boolean function then:

{% highlight scala %}
line => line.contains("Sale Stock")
{% endhighlight %}

Ahh interesting, `line` is the input parameters and it returns a boolean value from `line.contains("Sale Stock")` one. And that's part is a [Scala Anonymous Function](http://docs.scala-lang.org/tutorials/tour/anonymous-function-syntax.html).

It seems, Scala is have a nice syntax to express the anonymous function. I can express previous function as:

{% highlight scala %}
val isContainsSaleStock = (s: String) => s.contains("Sale Stock")
val lineWithSaleStock = textFile.filter(isContainSaleStock)
{% endhighlight %}

This [post](http://docs.scala-lang.org/tutorials/tour/anonymous-function-syntax.html) from Scala Doc provides good resources about Scala anonymous function.
