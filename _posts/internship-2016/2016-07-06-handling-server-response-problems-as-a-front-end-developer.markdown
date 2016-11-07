---
author: agarwali
comments: true
date: 2016-07-06 21:34:31+00:00
layout: post
title: Handling Server Response problems as a front-end developer
meta:
category: internship-2016
excerpt_separator: <!--more-->
media:
media_source:
---


_The back-end developer on my team is on vacation and I needed help with a certain part of the API that is still undocumented. In this post, I'm going to talk about how I arrived at this problem and how I solved it in the absence of the back-end developer._<!--more-->

The back-end on our project is made using Ruby on Rails. I have done back-end work before using python on Flask, and PHP but I just know some basics about ruby on rails. While I was working on a feature that will display the information of fields in the database that might be created in the future using JSONb, I needed an API route to check what future fields are present. Usually, all API routes are documented in a google doc that I use very often when making a function that makes HTTP requests. I could recall the back-end developer creating this routes from one of our conversations but unfortunately it was undocumented.

With some independent research, I figured that all API routes are placed in routes.rb file in the config folder of the rails app. I found an /extra_columns route that returned all the extra_columns in the database. So, I created an HTTP request to that path but I still could not retrieve the data. The status code from the response was OK, but I couldn't figure out why I couldn't extract the data. After spending some one hour I realized that the json response might have some key-value pair that I didn't know about. Then, I switched to PostMan which is a very useful tool for API developers that allows you to test your routes by make GET, POST, PATCH etc. requests to your API and checking your response. After some debugging and setting the header correctly I finally got a response from the server, where I found the key that I needed to extract the data.

I wish I had switched to PostMan in the beginning. It would have saved me some time and stress.
