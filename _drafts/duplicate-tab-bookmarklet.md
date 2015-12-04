---
title: Duplicating A Safari Browser Tab
layout: post
---

This is a little convenience bookmark I created for myself a while back. After being a long time user of the Chrome browser on the desktop, I found the lack of a way to duplicate a tab in Safari on iOS to be annoying.

So, I created a simple bookmarklet that I could save into Safari. It barely does anything, just opens the current URL in a new tab.

Here it is, in all it's tiny glory.

{% highlight javascript %}
javascript:(function(){window.open(window.location.href);})()
{% endhighlight %}