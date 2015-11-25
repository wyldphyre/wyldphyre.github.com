---
title: Introduction to - YouTubeDownloader
subtitle: automated downloading of YouTube videos makes my happy
layout: post
---

This is is my most recent Python scripting adventure and it came together quicker than I thought it would once I got started. If it sounds like something you'd like to use, you can find it [here on Github](https://github.com/wyldphyre/YouTubeDownloader).

Here's the story of how it came about, and how I have put it to use in order to solve a long standing annoyance problem.

## The Problem
For a long time (years in fact) I've wanted a way to automatically download YouTube videos so that I could watch them at my leisure without having to wait for them to buffer on my not so great internet connection. 

This desire was a combination several of things that came together to become a constant minor annoyance. 

What I wanted was: 

- to avoid buffering and low quality videos due to bandwidth constraints
- to avoid manually checking for new content for channels I follow
- to integrate my YouTube watching into the rest of my media watching experience.

## Some Background
 I have no real interest in having a permanent copy of the vast majority of things I watch on YouTube, but I had good reason to want to have videos downloaded ahead of time. Because my internet connection is typically quite slow during the times I'm most likely to want to watch anything on YouTube (usually in the evening) I'd either end up having to watch blurry low quality videos, or waiting annoyingly long times for the video to buffer, often both together.
 
 I could get around this to some degree my watching on my phone using mobile data, or my iPad tethered to my iPhone, but that solution was limited. I only have 1.5 GB of mobile data per month, and that would get chewed up quick enough watching video. Plus, ideally, I'd like to be able to watch the videos on the larger screen of my TV. 

## Dashed Hopes  &nbsp;&nbsp; (ᵕ̣̣̣̣̣̣﹏ᵕ̣̣̣̣̣̣)
There was a period of time several years back when YouTube provided a way to get an RSS feed of a YouTube channel. It wasn't easy, but it could be done. And I'm a big fan of RSS. Great! That's would be part of the solution to getting automation rolling.

But no. With an RSS feed you could add it to your feed reader of choice and get prompt notification of when new videos were available, but that didn't solve the downloading side of things. I'm sure there were tools around that could download the videos but I never found a good one in the little bit of looking I did. And it's kind of a moot point these days since as far as I can tell it's been practically impossible to get an RSS feed out of YouTube for the last couple of years. I guess they really want you to watch videos on the website or in one of their apps.

There are also a plethora of websites out there that offer to download YouTube videos for you. You provide the URL of the video and after a little while they give you a link to download the video. I've tried a few here and there, but they tended not to be very good, and they certainly didn't get my any closer to an automated system.

## A New Hope &nbsp;&nbsp; ヽ(^。^)丿
And then by chance I recently became aware of a nifty Python script called [youtube-dl](http://rg3.github.io/youtube-dl/). And what does this little beauty do? Why, it takes all the pain out of downloading YouTube videos (and many other sites apparently, but I haven't tried any of them). Usage is simple enough via the command line, but even better, they've built it to be easy to call as a component of a Python script, and provided a nice simple example of how to do so.

So this gets me thinking. I've written a few small, handy Python scripts before. I've got the remarkably useful [Workflow](https://workflow.is) app on my iOS devices. Yep, with those pieces I should be able to largely automate downloading of YouTube content and finally fulfil that dream of mine. Let's do this! ( ᐛ )و

*I may be exaggerating a little about how I felt, but only a little. I can actually get excited about automation and knocking out useful little tools. I'm weird like that.* (・∧‐)ゞ

## Making a Thing 
And so, after thinking about it off and on for several days, I sat down on Sunday the 8th of November, 2015, and *I made a thing*.

### The iOS Workflow
The first thing I need to download a video from YouTube is the URL of the video. I'm most likely to be on an iOS device when looking at YouTube, so I need a way to do that on iOS. The way I decided to accomplish this was by using the app [Workflow](https://workflow.is) to create a simple workflow that would save the contents of the clipboard to a file in a specific folder in my Dropbox.

> *The [Workflow app for iOS](https://workflow.is) is an awesome app for anyone who has an interest in automation and/or doing neat things on their iOS devices. Every time I think about what it can do I'm amazed that they built it and that Apple let it into the Appstore. If you've never heard of it then check it out. Even if you don't want to do anything with it right now, I think it's worth being aware of as you never know when you might need to do something fancy that it would be an excellent solution for. I should really do a post about it one day.*

With the workflow created the process for saving YouTube URLs on my iPhone or iPad becomes:

- Find the video in the YouTube app (or Safari if I had to)
- Copy the URL, which is a share option in the app
- Trigger the workflow to save the URL to Dropbox. The URLs are saved into a folder a time stamp for the name and '.queue' as the extension.

On my phone I have the workflow available in the widget view, so I can just slide it down from the top of the screen and activate it. On my iPad I tend to trigger the workflow by opening the Workflow app in a slide over panel. Both ways are quick and easy to get to.

Should I happen to be on my Mac instead of an iOS device when I come across a video I want to download I use a slightly more manual process that is still relatively quick:

- Copy the URL
- Open terminal and `cd` to the folder the files are stored in
- use the following command to create a file with the contents of the clipboard in it…

{% highlight bash %}
$ pbpaste > made_up_file_name.queue
{% endhighlight %}

I could certainly automate this process on the Mac to make it much quicker, but I haven't bothered just yet.

Once the URL has been saved to Dropbox, it's the scripts turn to go to work, but it needs a little help to do so.

### Glueing the Script and the Workflow Together
Once the YouTube URL is saved to my Dropbox, how will I get the python script to make use of it? I guess I could have the script always running and monitoring the folder, but that seems like a waste of time and CPU cyles.

I have a Mac Mini that is my desktop computer, and it's always running. I already have [Hazel](http://www.noodlesoft.com/hazel.php) running on the Mac Mini, doing a variety of things, so adding one more small task to it's list was a simple decision to make.

>*If you've never used Hazel, it's another app that is really great for helping to automate things on OS X.*

So I have Hazel monitor the folder in Dropbox into which the files containing the URLs are saved. When Hazel detects a new file in the folder it triggers my YouTubeDownloader script.

Which finally brings us to…

### The Script
The script itself isn't all that large. All the YouTube handling stuff is wrapped up by [youtube-dl](http://rg3.github.io/youtube-dl/), so I just had to surround it with enough logic to fit into the process that I'd pieced together.

The process is fairly straightforward. First there is a little bit of house keeping:

- Script gets run
- If a `running.lock` file exists in the target folder, the script exits
- If still running, then immediately create the `running.lock` file so no other instance can run

Now we can move on to processing files:

- Get a list of all the .queue files in the configured folder (hard coded in the script at this stage, because I can), and start handling them one at a time.
- For each file, get the URL out of the file and pass it to the `youtube-dl` code, which will download it to another hard coded folder in my `~/Movies` folder. Each movie will be placed inside a folder named after the name of the YouTube account that uploaded the file.
- When the download for a file is completed, rename the file extension to `.handled`.
- Once all the .queue files initially found have been dealt with, look for more files to process. If any are found, repeat the steps above, otherwise deleted the lock file and exit.

Here is the script as it exists at this point in time.

{% highlight python %}
#! /usr/bin/env python

from __future__ import unicode_literals
import os
import youtube_dl

# Use of youtube-dl  is based on the example provided at
# https://github.com/rg3/youtube-dl#embedding-youtube-dl


class Logger(object):
    def debug(self, msg):
        pass

    def warning(self, msg):
        pass

    def error(self, msg):
        print(msg)


def progress_hook(d):
    if d['status'] == 'finished':
        print('Done downloading, now converting ...')


def process_file(file_path):
    ydl_opts = {
        'outtmpl': '~/Movies/YouTubeDownloads/%(uploader)s/%(title)s.%(ext)s'
    }

    with open(file_path) as f:
        lines = [line.rstrip('\n') for line in f if line != '' and line != '\n']

        if len(lines) > 0:
            with youtube_dl.YoutubeDL(ydl_opts) as ydl:
                ydl.download([lines[0]])


def youtubedownloader():
    queue_path = '/Users/craigreynolds/Dropbox/Apps/YouTubeDownloader/'
    lock_path = os.path.join(queue_path, 'running.lock')

    if os.path.exists(lock_path):
        exit()

    lock_file = open(lock_path, 'w+')
    lock_file.close()

    directory_list = os.listdir(queue_path)
    queue_files = [file.rstrip('\n') for file in directory_list if file.endswith('.queue')]

    while len(queue_files) > 0:
        for filename in directory_list:
            file_path = os.path.join(queue_path, filename)

            if filename.endswith('queue'):
                process_file(file_path)
                os.rename(file_path, file_path.replace('.queue', '.handled'))

        directory_list = os.listdir(queue_path)
        queue_files = [file.rstrip('\n') for file in directory_list if file.endswith('.queue')]

    os.remove(lock_path)


youtubedownloader()
{% endhighlight %}


## Handling the Downloaded Files
At this point I have a folder, `~/Movies/YouTubeDownloads/`, that contains one or more subfolders (named for the YouTube account), and those subfolders contain one or more videos. That's nice, but they aren't in their final resting place. They still need to make it to another computer where I store all my media.

To achieve that I used Hazel once again. I added the folders of accounts I will download videos from at least semi-regularly into Hazel, and told it to move any video files it finds in those folders to a new location in my media store. For accounts I don't regularly download from, it's not that big a deal to move files by hand.

## Housekeeping
In order to prevent the Dropbox folder from filling up with superfluous files I have Hazel automatically delete any files with a `.handled` extension that are more than 3 days old.

## Conclusion
So, after all that my solution is:

- Copy URL to YouTube video on iPad or iPhone
- Trigger the workflow to save URL to file in Dropbox, which syncs to my Mac Mini
- Hazel and my YouTubeDownloader script will run on the Mac Mini to download the video
- Hazel will automatically move most files into my media store, where they will be waiting for me to watch them.

It works surprisingly well. I was half expecting to run into some kind of hiccup in the process, but it all came together rather smoothly, and I'm quite happy with the resulting ease of use. I've been using it for about three weeks now and it hasn't missed a beat. 

I expect I'll tweak it and refine it over time, but it's a great start.