---
author: agarwali
comments: true
date: 2016-06-29 02:27:47+00:00
layout: post
title: Using SASS vs CSS
meta:
category: internship-2016
excerpt_separator: <!--more-->
media:
media_source:
---

Today, I switched from using CSS to SASS, which is a CSS preprocessor. In the beginning, I was very reluctant to add that extra bit of complexity in my workflow. Go away!<!--more-->But today, I changed my mind. SASS or SCSS can be a very powerful ally of a front-end developer. As a newbie in front-end engineering, it is very hard to learn everything about CSS, and it is the only thing I spent most of my time writing, and tweaking div's in developer tool to ensure the final product meet the requirements or follow a style guide as I mentioned in my last blog post. Even if you are following a style guide now, things can change in the future, or maybe you want to redesign your application, or your company is doing a rebranding. In these events, it is definite that you have to change the value of background-color in multiple places. It might even be horrifying to find that particular file.  Don’t you wish CSS allowed you to use predefined variables that you could use in multiple places like any other programming languages ? Well, SASS or SCSS allows you to do exactly that.


    <span class="token selector">$brand-color: #fff;
    .btn </span><span class="token punctuation">{</span>
    <span class="token property">  color</span><span class="token punctuation">:</span> $brand-color<span class="token punctuation">;
    </span><span class="token punctuation">}
    </span><span class="token selector">nav </span><span class="token punctuation">{</span>
    <span class="token property">  background-color</span><span class="token punctuation">:</span> $brand-color<span class="token punctuation">;
    </span><span class="token punctuation">}</span>


It allows you to do other amazing things such as write small snips of SASS in multiple files and import them in one file. You can also define a common style of an element and extend that style if a certain class is added to that element. More can be found at [SASS documentation.](http://sass-lang.com/guide)

CSS is not easy, but SASS is also not a completely alien language. It has some of its own syntax, but it can largely be written just like one would write CSS. It definitely makes the life of a front-end developer like me easier  without interfering with my workflow and I love using it.
