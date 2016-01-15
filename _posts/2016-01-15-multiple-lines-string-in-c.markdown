---
layout: post
title:  "Multiple Lines String In C"
date:   2016-01-15 09:01:48 +0700
categories: c
---
There are two ways of splitting `char *` variable in mupltiple lines.

    /* the first one */
    char *str1 = "line 1\n \
    line 2";

    /* the second one */
    char *str2 = "line 1\n"
                 "line 2";

I like the second one.

It can be useful for printing multple lines in C. Let's take a look redis source code as an example. Instead of printing multiple lines string like this

{% gist pyk/f13134a1a33b1634fde0 redis-usage.c %}

I like to write the code like this one

{% gist pyk/f13134a1a33b1634fde0 redis-usage-alt.c %}

less typing FTW.