---
author: agarwali
comments: true
date: 2016-04-08 13:54:53+00:00
layout: post
title: First Pull Request to an Open Source Project
meta:
category: foss
excerpt_separator: <!--more-->
media:
media_source:
tags:
- community
- FOSS
- octoprint
- opensource
- pullrequest
- software
---



This is about how submitting my first pull request to [OctoPrint](http://octoprint.org).

Yes, it is a great feeling to able to contribute to an open source project, and I am cherishing these feelings as I write this blog post. I don't want to be poetic here, but I'm feeling a little accomplished after all my efforts, and struggle I went through to<!--more--> [contribute](https://iamishwar.wordpress.com/2016/01/20/getting-started-with-contributing-to-open-source-software/) to an Open Source project. You might want to try submitting a pull request to an Open Source project, to sense the same feelings.




### Testing and Final Touches.


Technically, I should have written another post this week but I'm going to quickly summarize what [Kye](http://hooverkblog.wordpress.com) and I have been doing this week to submit our [first pull request](https://github.com/foosel/OctoPrint/pull/1306). If you were following my blog, in the last [post](https://iamishwar.wordpress.com/2016/04/04/building-the-right-ui-and-spotting-errors/), I talked about how we build the UI for implementing the layer up/down feature requested by issue [#1149](https://github.com/foosel/OctoPrint/issues/1149). Meanwhile, we spotted an error that was being caused by the on-key event-binding that was not disabled if the G-Code was not uploaded.So first, thing we did was created a jQuery function to add

First, we created a jQuery function to allow the buttons to trigger the Layer up/down scroll bar in the G-Code viewer as mentioned in the last post. Next, we disabled the button if the G-Code was not uploaded and enabled the button by refactoring the if-else statements to include the jQuery .prop() function as seen below. Changes are also visible in this [commit](https://github.com/agarwali/OctoPrint/commit/e5a8d4ad94d89d8316b3cd0b1aa9672555eb1ab1).


    if (!model) {
     self.ui_modelInfo("");
     if (self.layerSlider != undefined) {
      $('#btn_layer_up').prop('disabled', true);
      $('#btn_layer_down').prop('disabled', true);
     }
    }
    else {
     if (self.layerSlider != undefined) {
     $('#btn_layer_up').prop('disabled', false);
     $('#btn_layer_down').prop('disabled', false);
     }
    }


We tested this functionality using three test cases while having the printer connected and not connected.




  1. G-code was not uploaded


  2. G-code was uploaded


  3. G-code was uploaded and deleted.




### Debugging


We fixed the javaScript event-binding error we found by returning the event early if self.layerSlide was undefined. It was easy to accomplish with one line of code.


### Committing changes and submitting Pull Request


To submit a pull request we had follow OctoPrint's contributing Guideline. We had the repository forked already so, we committed our changes to a new branch dev/gcodeLayerButton and pushed our changes against the devel branch. We forgot to add ourselves to the AUTHORS.md file so we had to commit another change, and this might we be one of the reasons why our pull request might be rejected because the guidelines says to do 1 commit per pull request. But we went ahead and submitted the pull request, and we are hoping to hear back soon.


### What Next?


I'm planning on working on another issue before the semester comes to an end. It might be a little rushed, but I'm up for the challenge.

Keep following my blogs on [Open Source](https://iamishwar.wordpress.com/category/foss-engineering/) to be updated on my work.
