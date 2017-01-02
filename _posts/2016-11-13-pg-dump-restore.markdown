---
layout: post
title: "Postgres Dump and Restore"
date: 2016-11-13 20:07
comments: true
categories: [ postgres ]
---

This is more a note to myself because I always have to look this up.

{% highlight bash %}
pg_dump -Fc -h host -U user database > ~/tmp/database.dump
pg_restore -Fc -d target_database -O -x -1 ~/tmp/database.dump
{% endhighlight %}

* `-Fc` defines the PG custom format for the dump
* `-O` disables some owner set stuff
* `-x` disables the access right stuff
* `-1` ensures that everything is done in one transaction
