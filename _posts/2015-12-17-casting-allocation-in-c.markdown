---
layout: post
title:  "Casting Allocation In C"
date:   2015-12-18 05:48:08 +0700
categories: c 
---

If I allocate block of memory for the `obj_t` it's look like this

{% highlight c %}
obj_t *obj = (obj_t *)malloc(sizeof(obj_t));
obj_t *obj = (obj_t *)calloc(nmemb, sizeof(obj_t));
{% endhighlight %}

After reading [this post](https://gustedt.wordpress.com/2014/04/02/dont-use-casts-i/), I'm wondering why I use cast anyway?

My thought was because `malloc` and friends is returning `void *` so I need to cast to the appropriate type. 

And now if I ask myself "Why do you need to cast anyway? Is there any effect?". My answer was "I don't know". So I decide to doing some research about this.

I found this [StackOverflow](http://stackoverflow.com/a/605858/3376568) answer which provide excellent information about the bad of using cast for `malloc` and friends. 

This is a quick summary from that discusion

### Do I cast the result of malloc?

{% highlight text %}
No; you don't cast the result, since:

* It is unnecessary, as void * is automatically and safely 
promoted to any other pointer type in this case.

* It can hide an error, if you forgot to include <stdlib.h>. 
This can cause crashes (or, worse, not cause a crash until 
way later in some totally different part of the code). 
Consider what happens if pointers and integers are differently 
sized; then you're hiding a warning by casting and might 
lose bits of your returned address.

* It adds clutter to the code, casts are not very easy to 
read (especially if the pointer type is long).

* It makes you repeat yourself, which is generally bad.
{% endhighlight %}

It's turnout that `cast` is a harmful, I should avoid them as much as possible.

### Is there any effect using cast?
{% highlight text %}
It's a failure to include the cast, even if you got it right. 
There are simply no benefits to doing it, but a bunch of 
potential risks, and including the cast indicates that 
you don't know about the risks.
{% endhighlight %}

Well, 100% Agree.

### The last one
{% highlight text %}
To add further, your code needlessly repeats the type information
(int) which can cause errors. It's better to dereference the 
pointer being used to store the return value, 
to "lock" the two together:

int *sieve = malloc(length * sizeof *sieve);

This also moves the length to the front for increased visibility, 
and drops the redundant parentheses with sizeof; they are only 
needed when the argument is a type name. Many people seem to 
not know (or ignore) this, which makes their code more verbose.
Remember: sizeof is not a function! :) 
{% endhighlight %}

"It's better to dereference the pointer being used to store the return value"

## Conclusion
I don't cast allocation anymore and use dereference the pointer instead of type name as an argument of `sizeof`.

{% highlight c %}
obj_t *obj = malloc(sizeof *obj);
obj_t *obj = calloc(nmemb, sizeof *obj);
{% endhighlight %}

The good news is it also improve my code to be more readable.