---
layout: post
title:  "Supreme C"
date:   2016-01-22 10:24:10 +0700
categories: c
---

Lately, I've been thinking about consistency in C programming language API. Honestly, for me [Go Programming Language](https://golang.org) is very well designed. Not to mention that a bunch of smart peoples are behind it.

I like Go interface, I like how to Go handle an error, awesome standart libraries, awesome communities, etc. I would like to write in C and feels like to write Go code. Can I have it?

Right now, I have an idea to create an simple, consistent, and high-level C programming language API. I called it "Supreme C". In case you curious, "Supreme C" I take from [Supreme Chancellor](http://starwars.wikia.com/wiki/Supreme_Chancellor) name.

I would like to have an API that handle a low level stuff for netoworking, so I can use a function like `connect("localhost:8080")` and socket file descriptor ready to read and write is returned.

I want to write and read buffer safely. So, using `io.Reader` and `io.Writer` concept from Go programming language is a good idea.

Maybe I will start building Supreme C from the problem that I need to solve. But, I already have the big picture. Supreme C will look like a standart Go library.




