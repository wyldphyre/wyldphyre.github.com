--
title: An Introduction To the Goodreads Amazon Search Bookmarklet
layout: post
--

This is a perfect example of a situation where I had a personal annoyance and created a solution to scratch my itch.

# What it does

When you are viewing a book on the [Goodreads](http://www.goodreads.com) website you can trigger this bookmarklet and it will open an Amazon search in a new tab, using the title and author of the book you were looking at as the search criteria. In the case where a book has more than one author, only the first author is used in the search criteria.

Because I use the Australian Amazon website, the bookmarklet works with the Australian site! However that can be easily changed by tweaking the URL in the bookmarklet.

# Why I made it

I created this bookmarklet after several times finding myself on the [Goodreads](http://www.goodreads.com) website and wanting to look up a book on Amazon, but being frustrated that of the search options that Goodreads provided, an Amazon search was available. You have to to open an Amazon page and search yourself, entering booking information by hand to do a search. After doing this several times I found that it was more annoyance than I was willing to put up with, so after a small amount of effort that I put together this bookmarklet.

# The Code

```javascript
javascript:(function(){
    var bookTitle = document.getElementById("bookTitle").firstChild.data;
    var firstAuthor = document.getElementsByClassName("authorName")[0].firstChild.innerHTML;
    var titleAndFirstAuthor = (bookTitle.trim() + " " + firstAuthor).replace(/\s/g, "+");

    window.open("http://www.amazon.com.au/s/ref=nb_sb_noss?url=search-alias%3Daps&field-keywords=" + titleAndFirstAuthor);})()
```