---
layout: post
title:  "Scala on Debian"
date:   2016-04-09 12:54:00 +0700
categories: scala, debian
---

Just dig deeper on [Scala](http://www.scala-lang.org/) world. I leave a note
here on how to setup Scala on debian.

Choose Scala version [here](http://www.scala-lang.org/download/all.html), 
I use [Scala 2.12.0-M3](http://www.scala-lang.org/download/2.12.0-M3.html) one. Grab the download link of debian package.

{% highlight text %}
http://downloads.lightbend.com/scala/2.12.0-M3/scala-2.12.0-M3.deb
{% endhighlight %}

And now, setup using the following command:

{% highlight shell %}
wget http://downloads.lightbend.com/scala/2.12.0-M3/scala-2.12.0-M3.deb
sudo dpkg -i scala-2.12.0-M3.deb
{% endhighlight %}

Try it, make sure it works

{% highlight shell %}
% scala
Welcome to Scala 2.12.0-M3 (Java HotSpot(TM) 64-Bit Server VM, Java 1.8.0_72).
Type in expressions for evaluation. Or try :help.

scala> 2 + 2
res0: Int = 4
{% endhighlight %}
