---
author: agarwali
comments: true
date: 2016-02-24 07:01:03+00:00
layout: post
title: 'Problem Identification: First deep dive'
meta:
category: foss
excerpt_separator: <!--more-->
media:
media_source:
---



This post is about a problem I identified through the OpenMRS issue queue that I think would be a good way to dig deeper into OpenMRS.
<!--more-->

## Confessions


First, I have to admit that I have not been blogging lately. I have been working on two OpenMRS modules project. I have been trying to create the hello-openmrs module using the maven archetype as well as creating another module which is dependent on the UI framework module that allows anyone to build custom user interfaces. The only reason I started working on UI framework module is because of an issue I had identified in the OpenMRS introductory issue queue.


## The Problem


[UIFR-124 Log Errors that are being captured on screen](https://issues.openmrs.org/browse/UIFR-124) is one of the issues I have tracked down last week. It is not a bug, but a very important feature that needs to be implemented. According to my understanding from the description of the issue, we need to log errors caught by the UI Framework module using the standard OpenMRS logger mechanism.

<!-- more -->

To understand the error we need a little background on the UI Framework module. This is a structure that is used to create user interfaces fast and easily. Pages and fragments are created using Groovy which is managed through a page controller and fragment controller that makes the user interface dynamic. This is my most basic understanding, but I could be wrong.

I am assuming that to implement this feature, we do not need to understand everything about UI framework. My assumption is based on of the lines reported in the issue UIFR-124 description: "There is(already) a  capture all mechanism in pages loaded via ui framework mechanisms that will display errors and their stack traces on the screen, but will not log them to log files."

This is true because I have identified the portion of code that both [catches the exceptions ](https://github.com/openmrs/openmrs-module-uiframework/blob/a0a5545988cb40b097312a67e19fba819da21f90/omod/src/main/java/org/openmrs/module/uiframework/PageController.java)and [displays them on the screen](https://github.com/openmrs/openmrs-module-uiframework/blob/a0a5545988cb40b097312a67e19fba819da21f90/omod/src/main/webapp/uiError.jsp).

The problem looks very straightforward. I have asked for some clarification in the comment section on how does usually OpenMRS log errors in file, and I am hoping I get a response soon. Meanwhile, I will keep researching on module creation.
