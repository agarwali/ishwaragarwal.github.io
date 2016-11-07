---
author: agarwali
comments: true
date: 2016-04-04 14:36:21+00:00
layout: post
title: Building the right UI and spotting errors
meta:
category: foss
excerpt_separator: <!--more-->
media:
media_source:
---

Continuing from the responses we received from our last [work ](https://iamishwar.wordpress.com/2016/03/30/responses-from-the-octoprint-community/)on issue [#1149](https://github.com/foosel/OctoPrint/issues/1149#issuecomment-205282095), Kye and I started working on the buttons and went through several iterations to come with the best UI possible without breaking already existing functionality.

<!--more-->
![OctoPrint-GCode-Viewer](https://iamishwar.files.wordpress.com/2016/03/octoprint-gcode-viewer.png)Our first idea was to just add an extra div that will contain two buttons at the top of the G-Code canvas div. However, we were facing some issues with it. The div pushed the down the g-code canvas layer, but it did not push the layer slider with it. So, the button's div and the layer slider div were overlapping. Another idea was to put two small arrows on top and bottom of the layer slider. We did, not choose this option because the main purpose of the buttons was to be used in mobile and tablets. If the buttons were too small they would not be useful in small devices.

![Screenshot from 2016-04-04 00:18:38](https://iamishwar.files.wordpress.com/2016/04/screenshot-from-2016-04-04-001838.png)



So, we put the buttons at the bottom of the horizontal slider. This was easy to implement because we did not have to worry about the layout of other sliders and the G-code canvas. We changed the style to span to the width of the entire G-code canvas, so the buttons seemed a part of the canvas rather than an extra entity.



We then used jQuery and JavaScript to create the function calls to change the value of the layer slider.

$( "#btn_layer_up" ).click(function() {
var value = self.layerSlider('getValue');
self.layerSlider.slider('setValue', value+1);
});
$( "#btn_layer_down" ).click(function() {
var value = self.layerSlider('getValue');
self.layerSlider.slider('setValue', value-1);
});

While working on this issue we discovered and error, in the on-key layer up and down functionality. It wasn't disabled if the there was no G-code uploaded, which triggered errors in the console because the on-key up and down was trying to move a disabled layer slider.

We posted the screenshots in the issue ticket to get feedback from the community and reported the issue as well. We start cleaning the code and submit a pull request as soon as we get a response back.
