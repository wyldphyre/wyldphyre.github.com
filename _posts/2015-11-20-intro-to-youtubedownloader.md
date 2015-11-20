---
title: Introduction to - YouTubeDownloader
subtitle: automated downloading of YouTube videos makes my happy
layout: post
---

This is is my most recent little Python scripting adventure and it came together quicker than I thought it would once I started.

For a long time (years in fact) I've wanted a way to automatically download YouTube videos so that I could watch them at my leisure without having to wait for them to buffer on my not so great internet connection. The automation I have at the moment isn't perfect, but it it's pretty good, and is nice an flexible. This desire is a combination of things: desire to avoid buffering and low quality videos, desire to avoid manually checking for new content for channels I follow, desire to integrate my YouTube watching into the rest of my media watching experience.

Here's how it came about.

## Some Background
 I have no real interest in having a permanent copy of the vast majority of things I watch on YouTube, but I had good reason to want to have videos downloaded ahead of time. Because my internet connection is typically quite slow during the times I'm most likely to want to watch anything on YouTube (in the evening, for example) I'd either end up having to watch blurry low quality videos, or waiting annoyingly long times for the video to buffer, often both together.
 
 I could get around this to some degree my watching on my iPhone, or my iPad tethered to my iPhone, but that solution was limited. I only have 1.5 GB of mobile data per month, and that would get chewed up quick enough watching video. Plus, ideally, I'd like to be able to watch the videos on the larger screen of my TV. 

## Dashed Hopes (ᵕ̣̣̣̣̣̣﹏ᵕ̣̣̣̣̣̣)
There was a period of time several years back when YouTube provided a way to get an RSS feed of a YouTube channel. It wasn't easy, but it could be done. And I'm a big fan of RSS. Great! That's looks like part of the solution to getting automation rolling.

But no. With an RSS feed you could add it to your feed reader of choice and get prompt notification of when new videos were available, but that didn't solve the downloading side of things. I'm sure there were tools around that could download the videos but I never found one in the little bit of looking I did. And it's kind of a moot point these days since as far as I can tell it's been practically impossible to get an RSS feed out of YouTube for the last couple of years. I guess they really want you to watch it on the website or in one of their apps.

There are also a plethora of websites out there that offer to download YouTube videos for you. You provide the URL of the video and after a little while they give you a link to download the video. I've tried a few here and there, but they tended not to be very good, and they certainly didn't get my any closer to an automated system.

## A New Hope ヽ(^。^)丿
And then by chance I recently became aware of a nifty Python script called [youtube-dl](http://rg3.github.io/youtube-dl/). And what does this little beauty do? Why, it takes all the pain out of downloading YouTube videos (and other sites apparently, but I haven't tried any of them). Usage is simple enough via the command line, but even better, they've built it to be easy to call as a component of a Python script, and provided a nice simple example of how to do so.

So this gets me thinking. I've been a professional developer for over a decade. I've written a few small, handy Python scripts before. I've got the remarkably useful [Workflow](https://workflow.is) app on my iOS devices. Yep. Those are all the pieces I should need to be able to largely automate downloading of YouTube content and finally fulfilling that dream of mine. Let's do this! ( ᐛ )و

*I may be exaggerating a little about how I felt, but only a little. I can actually get excited about automation. I'm weird like that.* (・∧‐)ゞ

## Making a Thing 
And so, after thinking about it off and on over the period of several days, I sat down on Sunday the 8th of November, 2015, and I made a thing.

### The Script
*describe the script here*

### The iOS Workflow
As mentioned above, the YouTubeDownloader.py script needs source files in order to work. The Workflow app is how I create those files on an iOS device, which is mostly where I look at YouTube.

> *The [Workflow app for iOS](https://workflow.is) is an awesome app for anyone who has an interest in automation and/or doing neat things on their iOS devices. Every time I think about what it can do I'm amazed that they built it and that Apple let it into the Appstore. If you've never heard of it then check it out. Even if you don't want to do anything with it right now, I think it's worth being aware of as you never know when you might need to do something fancy that it would be an excellent solution for. I should really do a post about it one day.*

In order to get a YouTube URL into my script I created a workflow that would save whatever was on the clipboard into a file in a specified folder in my Dropbox.
 *describe the workflow here*