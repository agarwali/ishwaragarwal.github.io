---
author: agarwali
comments: true
date: 2016-06-13 03:24:23+00:00
layout: post
title: Material Design Library for Angular 2
meta:
category: internship-2016
excerpt_separator: <!--more-->
media:
media_source:
tags:
- angular2
- materialdesign
- materializecss
---


_This post is about the material design library I have chosen for my Angular 2 project I'm working on and why I chose that library._

At Interapt, we follow Material Design principles very closely. Our designers have developed a set of design guidelines that are build upon Material Design language developed by Google. According to Google, Material is a visual language for users that synthesizes the classic principles of good design with the innovation and possibility of technology and science. More about Material Design can be found in this living [spec](https://material.google.com/).

<!--more-->

I think Material Design provides a unified experience across all platforms and devices. When applications are built using material design, it almost seems that it has come to live. Visual cues such as dark and ambient shadows, motion, tactile feature, and bold international graphics provide a meaning to the design.

AngularJS, has a stable a material design library that can when DOM elements are rendered dynamically. Angular 2 developers have released an alpha version of its Material Design library, but is not stable yet and there are some very important components that are yet to be developed. This left me to choose between three widely used material design library, Material Design Lite (MDL), Materialize CSS, and Materialize-UI.

I started with experimenting with MDL, and soon realized that when DOM elements where dynamically rendered, the MDL styles and properties were not applied to markup. So I had to create a custom directive that would rerun the script of the library after a view was initialized in Angular 2. This worked but I realized as my application would get bigger I would have to add a lot of custom directives, leading to more error.

But, then I found Materialize CSS and a library called Angular 2 Materialize that comes with a package of directives that allows one to use the components of Materialize CSS library. It was easy to install and all the instructions can be found in the readme of the [GitHub repository](https://github.com/InfomediaLtd/angular2-materialize). Other benefits of using Materialize CSS are that it is very light weighted, heavily customizable, and has more components that MDL.
