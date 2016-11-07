---
author: agarwali
comments: true
date: 2016-04-20 14:54:28+00:00
layout: post
title: Tackling another issue on OctoPrint
meta:
category: foss
excerpt_separator: <!--more-->
media:
media_source:
---


We tracked down issue #1026 and now we know what he have to do to fix this issue.
<!--more-->

### What is the issue?


Joseph, Kye, and I have started working on issue [#1026](https://github.com/foosel/OctoPrint/issues/1026) on OctoPrint after Kye and I completed the [pull request](https://github.com/foosel/OctoPrint/pull/1306) on issue [#1149](https://github.com/foosel/OctoPrint/issues/1149). Issue #1026 is a feature request that involves G-code. G-Code is a generic name for control language for CNC machines, 3D printers etc. There is a terminal in OctoPrint app that allows users to submit G-code commands directly to control their printer. The issue is: "If you type a G-Code command with no arguments into the terminal page, it works whether the letter is upper or lower-case(g28 and G28 both works). Commands with multiple arguments only work if each letter is uppercase. (M280 P0 S150 works, m280 p0 s150 does not)".


### What do we need to do?


We could automatically upper-case every single command but there is a catch. There is some G-code commands,  `M117 `command, for example, can be used to send arbitrary text to be displayed on the printer's LCD, and that certainly should not be upper-cased.

After several back and forth conversation between community members one of the members posted what we need to do in a nutshell:Add new config setting: blacklist of commands to




  1. Add new config setting: blacklist of commands to _not_ completely auto-uppercase (incl. setting dialog, M117). It would probably fit into the "Advanced Options" section on the Serial tab of OctroPrint settings.


  2. Adjust `sendCommand` method of the `TerminalViewModel, `extract the G-code, and match against the blacklist. For the matches only upper-case G-code, and for non-matches uppercase full command before sending.




### Tracking the issue


The best way to figure out how to implement this feature is to track how similar features were already being accomplished. Below is a screenshot of the Advanced Options settings dialog.

![Screenshot from 2016-04-18 10:37:21](https://iamishwar.files.wordpress.com/2016/04/screenshot-from-2016-04-18-103721.png)

To create a blacklist of G-Code commands that should not be automatically uppercased we had to something very similar to the Long running commands in the settings dialog. So we started with tracing the files. It took us a while to figure out how the data was being posted and updated in the background. But I was able to use some debugging methodologies, like chrome dev tools, console.log() and python print statements to figure out the flow of data.

Front-End




  1. [**serialconnection.jinja2**](https://github.com/foosel/OctoPrint/blob/master/src/octoprint/templates/dialogs/settings/serialconnection.jinja2) - This is the advanced options windows in which we need to put our stuff.


  2. [**settings.js** ](https://github.com/foosel/OctoPrint/blob/master/src/octoprint/static/js/app/viewmodels/settings.js)- This is where the JavaScript is located, that holds the value of the fields in the advanced options and communicates with the server with GET/POST methods.


Backend




  1. [**server/settings.py**](https://github.com/foosel/OctoPrint/blob/692166f067329cd3d6fdc84389e0dd76184c5e0c/src/octoprint/server/api/settings.py) - Contains api/settings decorators that has get and post functions to send data back and forth between front end.


  2. **[settings.py](https://github.com/foosel/OctoPrint/blob/692166f067329cd3d6fdc84389e0dd76184c5e0c/src/octoprint/settings.py)** - Here is where the settings class is defined with set and get methods that receive data from default settings dictionary and update config.yaml


Documentation


  1. **[docs/configuration/config_yaml.rst](https://github.com/foosel/OctoPrint/blob/692166f067329cd3d6fdc84389e0dd76184c5e0c/docs/configuration/config_yaml.rst)** 


We will also need to work with this [file](https://github.com/foosel/OctoPrint/blob/692166f067329cd3d6fdc84389e0dd76184c5e0c/src/octoprint/util/comm.py) that has the sendCommand method for the TerminalViewModel where we have to extract the G-code.

We are currently almost done with the first part of our issue. I'll be posting more as we move forward with this issue.
