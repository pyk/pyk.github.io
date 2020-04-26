---
layout: post
title:  "Hot Reload & Fast Local Development for AWS Lambda"
date:   2020-04-26 10:15:00 +0700
categories: aws, aws lambda, aws sam, serverless
---

This is myfirst time using AWS Lambda development tool.

I use the following command to start the development server locally:

{% highlight sh %}
sam local start-api
{% endhighlight %}

If you previously run build, the reload server will not work. 

Use the following command to force AWS SAM use your local version, not a build version:

{% highlight sh %}
sam local start-api -t template.yaml
{% endhighlight %}

If you changes your function, your server will be automatically reloaded.

By default, AWS SAM will pull docker image on every request. It will very slow.

Use the following command to speed up the local server:

{% highlight sh %}
sam local start-api -t template.yaml --skip-pull-image
{% endhighlight %}

This option `--skip-pull-image` will skip docker pulling image on every request.

That's it. Now you have hot reload & fast local development server for AWS Lambda.

