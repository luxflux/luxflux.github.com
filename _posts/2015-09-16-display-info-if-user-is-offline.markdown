---
layout: post
title: "Display Info if User is Offline"
date: 2015-09-16 23:54
comments: true
categories: [ javascript ]
---

In a web project we recently had the use case that user will need access to some important info on the website
when they are offline.

<!-- more -->

## HTML5 cache manifest

My first thought was to do this with a [HTML5 cache manifest](http://www.html5rocks.com/en/tutorials/appcache/beginner/).
Unfortunately, you can't use the FALLBACK section of the manifest without the caching part
As I also did not want to open the Pandora's box caching, I had to look for another option.

## Online- / Offline Events

After some research I came across the Javascript [Online- / Offline
Events](https://developer.mozilla.org/en-US/docs/Online_and_offline_events) on `window`.
By using `offline` we can display the information when the internet connection fails.
As soon as there is an internet connection, we can return.

As we are using [Turbolinks](https://github.com/rails/turbolinks) in our project, it became quite easy to
handle this.

{% highlight coffeescript %}
jQuery ->
  $.ajax '/offline'
    .done (data) ->
      $(window).on 'offline', (event) ->
        Turbolinks.replace data

      $(window).on 'online', (event) ->
        setTimeout ->
          location.reload()
        , 4000
{% endhighlight %}

This small example just fetches the page `/offline` via AJAX. If this is successful, it adds another two hooks
to replace the page content and reloading the page.

As the internet connection has to settle down, there is a timeout before reloading the page.

## Optimizations

As this solution calls `/offline` on every request, we add a lot of request which aren't necessary often.
I am sure you could use `localStorage` to cache the content and fetch it again once in a while.
