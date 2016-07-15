--
title: An Introduction To Slayer
layout: post
--

Like so many handy utility applications, Slayer is something I created to scratch my own itch. I work as a developer and periodically find myself needing to kill a process. The processes I want to kill are early always one of a handful that I work with regularly. Slayer makes it easy for me to kill these processes. I could certainly do what it does by hand, but this saves me time and annoyance.

# Background

My work as a Windows developer means that I often find myself needing to kill a process that may have stopped responding or won't close properly. We already had a simple tool to do this at work, but it was very basic and brute force, as it would kill all instances of a process, based on the executable path. I found that didn't work well for me, because I might often have multiple instances of an application running and I would rarely want to kill all instances at once. So I built my own improved version of an application killer. The old app was called *Killer*, so I called my app *Slayer*!

# What does it do?

The primary goal of Slayer is to make it quick and simple to deal with the scenario where I want to kill an application process when there are multiple instances of that application running. In that case, the UI will allow me to quickly kill only the process I want to kill, leaving the other process(es) to continue running uninterrupted. The functionality set has expanded a little from that initial goal, but it still maintains that focus. Should I happen to want to kill all instances of an application, that is also quick. All actions are a single button press once the UI has loaded.

# How does it work?

Slayer can be used in a command line fashion, but it primarily intended to be pinned to the Windows task at where it is always available she you want it. After the first time the application is run its jump menu is populated (right-click on the task bar button), providing quick access to kill any of the processes that have been configured in the settings file. The default settings contain several of the processes I personally have to deal with at work, but these are easily customised to whatever you need them to be by editing an XML file.

When several processes have bee configured, one of them can be set as default. That process will be the one that Slayer will operate on when run by clicking k the task at button. If there are multiple instances of that process running then you will see the UI so you can decide what to do. When there is only a single instance of a process that instance will be killed without showing the UI, unless you configure the UI to always show for that process. If you make the UI always appear the it turns killing processes into at least a two click process. Which is useful if you wish to avoid accidentally killing a process by clicking on the song task at button, which we all do from time to time (́▽`*)ゝ.

Here's an example of what Slayer looks like in my most typical use case.

![Slayer ready to kill two instances of Delphi 5]({{site.url}}/assets/slayer_example.png)

# Points of interest?

# Conclusion