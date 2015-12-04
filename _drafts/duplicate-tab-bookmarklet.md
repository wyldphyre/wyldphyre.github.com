---
title: Duplicating A Safari Browser Tab
layout: post
---

This is a little convenience bookmark I created for myself a while back. Having used the Chrome browser for some time on the desktop, I'd become a fan of the tab duplication command (right-click on the tab and select 'Duplicate'). When I started using Safari more on my iPad, I'd occasionally find myself wishing for the same functionality found the lack of a way to duplicate a tab in Safari on iOS to be annoying.

So I created a simple bookmarklet that would provide the same feature in Safari. It barely does anything, just opens the current URL in a new tab, but it's handy to have.

Here it is, in all its tiny glory.

{% highlight javascript %}
javascript:(function(){window.open(window.location.href);})()
{% endhighlight %}