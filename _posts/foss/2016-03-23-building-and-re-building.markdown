---
author: agarwali
comments: true
date: 2016-03-23 14:16:08+00:00
layout: post
title: Building and Re-building
meta:
category: foss
excerpt_separator: <!--more-->
media:
media_source:
---


This post is basically a summary of how I was finally able to setup the development environment and work on an issue.
<!--more-->

## Getting Started


After switching to OctoPrint, I have built the system several times. First, I have to admit that OctoPrint is very easy to build compared to OpenMRS. I started building it on cloud9 since it has a good shared environment for editing code. All I had to do is clone the repository, follow the instructions on the readme, and run OctoPrint server in the virtual environment.

<!-- more -->


## Rebuilding


Assuming that everything was working well, last week, my friend [Kye](http://hooverkblog.wordpress.com) and I were working on a feature request [#1142](https://github.com/foosel/OctoPrint/issues/1142). The feature requested was basically a bulk delete button for history files. One of the developers in the issue commented that the issue was taken care of using a plugin called FileManager. So, I tried installing the plugin and failed badly. When installing the plugin, using the Plugin Manager in OctoPrint, you provide the link to the repository of the plugin, and the rest of the work is done by itself according to the documentations. But I failed installing the plugin this way, because I wasn't able to provide sudo permissions. Then, I decided to install OctoPrint in the local environment, since I would have greater control on the permissions.


## Realization


It was very easy to build and run OctoPrint using the same instructions on the OctoPrint readme, but I failed to install the plug-in again because of mainly two errors 1)file permissions, and 2) dependency issues. This weekend, I wasn't able to


## Past-Weekend


This past weekend, I wasn't able to  work on OctoPrint since I was at Silicon Valley, California for a regional meetup of [University Innovation Fellowship](http://epicenter.stanford.edu/page/university-innovation-fellows) program I have been part of. To learn more about this follow my blog, and I will keep you updated on the work I have been doing to bring more Innovation and Entrepreneurship on campus.


## Trying to Resolve Issues


When I came back from California, I wanted to quickly get into OctoPrint development again. This is where my peers blogs became handy. I have been following Kye's blog from California. He uncovered that we should have been working on the [devel](https://github.com/foosel/OctoPrint/tree/devel) branch, which is apparently 600+ commits ahead of the master branch. Also, to resolve the permission issues, we should avoid using sudo during OctoPrint installation. Check out his blog post about [OctoPrint Development Setup](https://hooverkblog.wordpress.com/2016/03/21/octoprint-development-setup/) for details.


## What's Next?


Since issue #1142 is no longer an issue, Kye pointed out that to the OctoPrint community with a comment. Now, it is time to move on to another issue.
