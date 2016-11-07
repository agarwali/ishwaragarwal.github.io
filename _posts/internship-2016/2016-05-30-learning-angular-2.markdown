---
author: agarwali
comments: true
date: 2016-05-30 04:34:09+00:00
layout: post
title: Learning Angular 2 Part I
meta:
category: internship-2016
excerpt_separator: <!--more-->
media:
media_source:
tags:
- angular2
---


_This is my first post in the series of posts I'll be doing about Learning Angular 2. In this post,I'll briefly talk about the origin Angular _2,_ and compare Angular 2 with some other development tools and frameworks I have used thus far._ <!--more-->

Soon I came to realize that Angular JS is by far the most popular JavaScript framework for web application development. AngularJS was created, as a side project, in 2009 by two developers, Misko Hevery and Adam Abrons. The project was then adopted by Google to write much of their internal applications and it has been continually developed and maintained by Google engineers. (For the full history up until January 2014, see Hevery's [keynote from ngConf 2014](http://www.youtube.com/watch?v=r1A1VR0ibIQ)).

At the end of 2014, Google announced that Angular 2 would be a complete rewrite of AngularJS. Angular 2 uses TypeScript which is a superset of JavaScript is bringing true object oriented web development to the mainstream, in a syntax that is strikingly close to Java. The popularity of AngularJS or Angular 2 is in the fact that you can avoid the nightmare of writing and testing spaghetti jQuery code when building a single page application. In this blog, I'm going to give an overview of how Angular 2 works and what it means to build a single page application.

In contrast to an MVC (model-view-controller) framework like Java Spring, Ruby on Rails with HAML, I would say Angular 2 is a model-view-whatever framework. Yes, it is sole purpose is to write the client-side of applications and the server-side operations can be done any language and Angular 2 does not care about it. The data is communicated through a REST API, which would be a topic for another blog post. Nevertheless, assuming data is transmitted through GET or POST requests, Angular 2 handles the view through the use of components as opposed to a specific view being rendered by classical MVC frameworks.

In Angular 2 an application is a tree of loosely coupled components. For example, as you are reading this blog notice that the Navbar, Blog container, Sidebar, and Footer can each be visualized as separate components. Using the categories the navbar or clicking the next button you can navigate through different blog posts without reloading the entire page. The next blog would just float into the blog container area leaving the other components in its place. This creates a single page application where the user's experience is much richer as their views are not interrupted by page reloads.

In the next post, I will talk about the project I'd be working on this summer with other interns and how Angular 2 will come into play.
