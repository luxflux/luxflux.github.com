---
layout: post
title: "Postgres Dump and Restore"
date: 2015-09-16 23:54
comments: true
categories: [ javascript ]
---

This is more a note to myself because I always have to look this up.

## Creating the Dump

{% highlight bash %}
pg_dump -Fc -h host -U user database > ~/tmp/database.dump
{% endhighlight %}

## Restoring the Dump

{% highlight bash %}
pg_restore -Fc -d target_database -O -x -1 ~/tmp/database.dump
{% endhighlight %}
