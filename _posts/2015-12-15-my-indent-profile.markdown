---
layout: post
title:  "My indent(1) Profile"
date:   2015-12-15 16:16:24 +0700
categories: c code-format
---

Manage C codebase is not easy, especially if the project is team-based. One of the common issues is about consistency of code formatting. Keeping the consistency of code format is very hard, because the heterogonous of code editor and development environment.

This is where tools like `gofmt(1)` and `rustfmt(1)` used for. For C codebase there are common alternative: `clang-format(1)` and `indent(1)`. I use `indent` heavily. It's from GNU which is very simple and straight forward.

This is my `indent(1)` profile look like:

{% gist pyk/7e17494e49788edbe25d .indent.pro %}