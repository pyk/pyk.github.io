---
layout: post
title:  "The Rules of Buffer In C"
date:   2015-12-14 14:49:59 +0700
categories: c buffer
---

<p class="message">
    This rules does not cover of all buffer operation yet.
</p>

Buffer or String in C is represented as an array of `char` terminated by null character `\0`.

{% highlight c %}
char buff[6] = {'h', 'e', 'l', 'l', 'o', '\0'};

/* or */
char *buff = "hello"; /* \0 implicitly appended */

/* or */
char buff[] = "hello";
{% endhighlight %}

Null character is not the part of `buff` length but it does requires a memory space.

The problem is in the function for handling a string operation like allocation `malloc`, copy `strcpy(dest, src)` and concatination `strcat(dest, src)`  is performed in unsafe way.

`malloc` only allocate memory for us without initialize it which potentially have a garbage values (a values from previous operation that are not cleared). Where `strcpy` and `strcat` is assume that `dest` is big enough which lead us buffer overflow problem if the `src` is larger than `dest`.

This is a list of rules that I always follow when dealing with buffer

### 1. Allocation: Use calloc instead

{% highlight c %}
char *buff = (char *)calloc(LEN, sizeof(char));
{% endhighlight %}

`calloc` will allocate `LEN` contiguos block of memory with size `sizeof(char)`bytes for each block and initialize it to zero. This will make sure that `buff` is not contains any garbage values or sensitive information from the previous operation.

### 2. Copy: Use strncpy and terminate.

{% highlight c %}
char buff[6];
strncpy(buff, "helllo is extra hello", sizeof(buff) - 1);
buff[sizeof(buff) - 1] = '\0';
{% endhighlight %}

`strncpy` is copy all the first `sizeof(buff) - 1` from `src`. This help us prevent buffer overflow and corrupting the heap.

### 3. Concat: Use strncat

{% highlight c %}
char path[11];
char fname = "hello";
char *ext = ".txt";
strncat(path, fname, sizeof(path) - strlen(fname) - 1);
strncat(path, ext, sizeof(path) - strlen(ext) - 1);
{% endhighlight %}

This will make sure that the concat operation is not write to more than allocated memory for `path` buffer.

That's it.