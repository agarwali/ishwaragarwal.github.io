---
author: agarwali
comments: true
date: 2016-04-15 14:34:17+00:00
layout: post
title: Pull Request needed work
meta:
category: foss
excerpt_separator: <!--more-->
media:
media_source:
---

After submitting a [pull request](https://github.com/foosel/OctoPrint/pull/1306) on issue [#1149](https://github.com/foosel/OctoPrint/issues/1149), we received some feedback on our changes and what we need to fix for our pull request to be accepted.
<!--more-->
As I expressed in my last blog [post](https://iamishwar.wordpress.com/2016/04/08/first-pull-request-to-open-source-project/), I was really excited to be able to submit a pull request to OctoPrint. In two days we received feedback on our pull request, basically which meant that the pull request needs more work.

<!-- more -->


### No jQuery, Keep Calm and Use KO


One of the comments we received was for the use of jQuery directly in the code. I have been previously been confused for not being able to trace javaScript and jQuery because OctoPrint has done a good job of hiding jQuery and javaScript function calls by using the [knockout.js](http://knockoutjs.com/) library. This library provides all different methods for event handling, keeping the code very clean. It is very easy to mistake id's of elements in such a big software when using javaScript. The two main jQuery functions we used were:


    <span class="pl-en">$</span>(<span class="pl-s"><span class="pl-pds">'</span>#btn_layer_up<span class="pl-pds">'</span></span>).<span class="pl-en">prop</span>(<span class="pl-s"><span class="pl-pds">'</span>disabled<span class="pl-pds">'</span></span>, <span class="pl-c1">true</span>);
    <span class="pl-en">$</span>( <span class="pl-s"><span class="pl-pds">"</span>#btn_layer_up<span class="pl-pds">"</span></span> ).<span class="pl-c1">click</span>(<span class="pl-k">function</span>() {
    ....}


We had to replace this knockout's event listeners.

We defined a KO observable function, which is basically an event listener that updates the value of self.layerSelectionEnabled when a value is passed in it as parameter.


    <span class="pl-smi">self</span>.<span class="pl-smi">layerSelectionEnabled</span> <span class="pl-k">=</span> <span class="pl-smi">ko</span>.<span class="pl-en">observable</span>(<span class="pl-c1">false</span>) // defined event listener
    <span class="pl-smi">self</span>.<span class="pl-en">layerSelectionEnabled</span>(<span class="pl-c1">false</span>); // to change value
    <span class="pl-smi x x-first">self</span><span class="x">.inc</span><span class="pl-en x">rementLayer</span> <span class="pl-k x">=</span> <span class="pl-k">function</span>() {...} // to replace the click function




Then we had to bind the defined functions to the HTML


    <button id = "btn_layer_up" type="button" class="btn btn-primary btn-medium" style="width:48%" <span class="x x-first x-last">disabled='disabled'</span>> // old code
    <button id = "btn_layer_up" type="button" class="btn btn-primary btn-medium" style="width:48%" <span class="x x-first x-last"> data-bind = "click: incrementLayer, enable: layerSelectionEnabled"</span>> // new code


This change was easy to accomplish.


### Change function name


We were asked to change the name of the self.incrementLayer function to self.changeLayer because the name was misleading, as the function would both increase and decrease layers. After making this change we were in big trouble. Our entire button feature stopped working and we got console errors. After tracing javaScript for hours through developer tools, I discovered that a function called self.changeLayer was already defined. Whenever we called self.changeLayer it was triggering the function that was already defined above, giving us value errors. So we renamed our self.changeLayer again to self.shiftLayer and that fixed the issue.


### **Make text Translatable**


In our entire pull request, we used 4 words that were being shown in the frontend. OctoPrint supports the ability to translate to different languages. So we had to make the `Layer Up` text translatable. All we had to do is to wrap the text in `{{ _('...') }}`, so `{{ _('Layer up') }}` and `{{ _('Layer down') }}` could be detected and translated.

We committed our changes to the pull request branch and hoping to hear that our pull request was accepted. For now, I will continue to work on issue #1026.
