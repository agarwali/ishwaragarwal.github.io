---
author: agarwali
comments: true
date: 2016-03-30 13:49:50+00:00
layout: post
title: Responses from the OctoPrint community
meta:
category: foss
excerpt_separator: <!--more-->
media:
media_source:
---



Finally, I had the chance to test the software on a 3D printer. Thanks to [Ashley](https://aikenash.wordpress.com/) for helping us out with the connectivity. I was trying to recreate the issue [#1149](https://github.com/foosel/OctoPrint/issues/1149) as I had written in my last [blog post](https://iamishwar.wordpress.com/2016/03/28/almost-resolved-issue-1149/). In short the issue was about adding a layer up and down functionality in the G-Code viewer of OctoPrint. The feature request has two parts: 1) Add buttons for layer up/down 2) Add on-press-key event with the up and down keys. As soon as I commented on the issue ticket, I got some quick responses. One member had already worked on the on-press feature, so I wanted to test it.

<!--more-->


### Lessons from testing


While testing the connectivity of the printer, and the layer up and down feature, I learned two main things:




  1. You have to allow permissions to the OctoPrint group and users to access the USB port you will connect the printer with.


  2. Always do a git pull at the beginning of the day because we did not have the changes pushed by the last member, which was exactly the functionality we were trying to test.




### Reporting


So, the on-press feature worked well for the up and down keys. So, I reported back my findings to the community and asked if the buttons are still required. I got another quick response stating the buttons might be a good addition because some users might be using OctoPrint on their tablets or phones.


### TODO's and Challenges


Now, I have identified our TODO's and biggest challenges. We have to integrate buttons in the UI in this [**gcodeviewer.jinja2** ](https://github.com/foosel/OctoPrint/blob/master/src/octoprint/templates/tabs/gcodeviewer.jinja2)template for the G-Code viewer and edit the **[gcode.js](https://github.com/foosel/OctoPrint/blob/master/src/octoprint/static/js/app/viewmodels/gcode.js)** file to create an on-click function that will update the slider values. This is fairly simple, but the biggest challenge is to make it fit in the UI. The G-Code viewer layout is not as straightforward to port and shuffle. But, I'm currently working on the UI and keep following my posts to be updated.
