---
author: agarwali
comments: true
date: 2016-03-28 14:22:41+00:00
layout: post
title: 'Almost resolved issue #1149'
meta:
category: foss
excerpt_separator: <!--more-->
media:
media_source:
---

Last time I was working on issue [#1142](https://github.com/foosel/OctoPrint/issues/1142) with Kye, and we figured that this issue was resolved in a new plugin, which is in the development branch of OctoPrint, and yet to be released. The issue was marked as a milestone for OctoPrint 1.3 release.
<!--more-->!

![1142](https://iamishwar.files.wordpress.com/2016/03/1142.png)

Then Kye, Joseph and I started to work on issue [#1149](https://github.com/foosel/OctoPrint/issues/1149). This issue is a feature request for the G-code viewer in OctoPrint. G-Code viewer is a tab in the OctoPrint that allows users to see the 3D object layer by layer as seen in the picture below.

[OctoPrint-GCode-Viewer](https://iamishwar.files.wordpress.com/2016/03/octoprint-gcode-viewer.png)

The vertical slider allows users to slide through different layers of the 3D object. The issue is that it is sometimes difficult to select an exact layer you want in the G-COde viewer. The scroll bars generally work well, but having two buttons that allow you to click to move up and down a layer would be useful and more convenient in certain situations. In addition, if there was a support to use up and down keys to navigate through different layers would also be useful.



This seemed fairly simple. With some initial research, we figured out that the slider was implemented using JavaScript. In fact, they used a [bootstrap-slider](https://github.com/foosel/OctoPrint/blob/536bb31965db17b969e7c1c53e241ddac4ae1814/src/octoprint/static/js/lib/bootstrap/bootstrap-slider.js) library. We had two ways of implementing the solution: 1) Editing the library to add the buttons and up and down key functionality, or 2) Editing the [jinja ](https://github.com/foosel/OctoPrint/blob/master/src/octoprint/templates/tabs/gcodeviewer.jinja2)template and adding some JavaScript to the [gcode.js](https://github.com/foosel/OctoPrint/blob/master/src/octoprint/static/js/app/viewmodels/gcode.js) file. I knew that editing the library would not be a good choice because libraries always get updated and my changes would not stay. The second option seemed fairly simple because the bootstrap-slider has the option to get and set values. So, the following code could resolve the issue.


    <span class="pl-smi">var currentVal = <span class="pl-smi">self</span>.<span class="pl-smi">layerSlider</span>.<span class="pl-en">slider</span>(<span class="pl-s"><span class="pl-pds">"</span>getValue<span class="pl-pds">"</span></span>)
    self</span>.<span class="pl-en">nextLayer</span> <span class="pl-k">=</span> <span class="pl-k">function</span>() {
        <span class="pl-smi">self</span>.<span class="pl-smi">layerSlider</span>.<span class="pl-en">slider</span>(<span class="pl-s"><span class="pl-pds">"</span>setValue<span class="pl-pds">"</span></span>, currentVal<span class="pl-k">+</span><span class="pl-c1">1</span>);
    }


So, I posted on the issue page about the two ways the issue could be resolved. Unlike OpenMRS community, I got a reply in less than 24 hours. The contributor told me the second option was definitely easier and better approach. He also suggested the JavaScript code, which is almost exactly like the one I have written above.

I was happy because I was on the way to resolving an issue. But then something weird happened. Another contributor posted in the issue, saying they had already implemented the Up and Down key binding in the development branch, and that adding the button would not be a good option. The issue almost seems resolved even if I wasn't able to submit a pull request. However, I haven't tested the Up and Down key binding yet, because it would require me to use an actual 3-D printer. If I am able to test the solution and find that the Up and Down keys work then I can report back to the community to mark the issue as resolved. Otherwise, I would implement my solution.
