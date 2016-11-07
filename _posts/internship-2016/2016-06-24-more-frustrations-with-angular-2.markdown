---
author: agarwali
comments: true
date: 2016-06-24 02:10:54+00:00
layout: post
title: More frustrations with Angular 2
meta:
category: internship-2016
excerpt_separator: <!--more-->
media:
media_source:
---

Today, I learned another important lesson when working with cutting edge tools like Angular 2. Do not update your angular core library if you are not aware of the breaking changes.<!--more-->

So I've been building a web application with Angular 2 for about 3 weeks. In my last [post](https://iamishwar.wordpress.com/2016/07/25/problems-of-using-cutting-edge-technology/), I talked about some of the challenges I faced working with Angular 2 and how I dealt with them. But today I faced even greater challenges when I updated my angular 2 core library.

I wanted to connect the Angular 2 components I have created using different URI's. e.g. visiting myapp.com/form will display a form. I also wanted to restrict the access to certain URI's to logged in users only. Angular 2 has a router library that allows you to do that exactly. In the latest implementation of their router library, a developer can create an "AuthenticationGuard" class that implements the CanActivate class with a canActivate method, where one can check the conditions that will allow a user to access a certain route and return true or false. This class can be attached to any of the routes that the developer wants to protect.

However, this feature is only available in Angular 2 release candidate 3 (r.c.3) and I have been using r.c.1, so I needed to update my Angular 2 router package. When I tried to update the router library, it failed because it had several dependencies including the core needed to be updated to r.c.3. So without paying much attention I updated all the Angular 2 packages I was using to r.c.3. As soon as I updated all the libraries, "the code started screaming!!" Angular 2 r.c.3 has a lot of syntactical changes, which I was able to track down. But I hadn't realized that in r.c.3 the Angular team also released some major changes in the Angular 2 form library. So none of my form components were working anymore. The documentation was also not updated since this is a very recent change. Finally, I was able to find this Angular 2 [Changelog](https://github.com/angular/angular/blob/master/CHANGELOG.md) that lists all the breaking changes in their newer release candidate.

It was very frustrating to track down all the errors produced by this update. However, by breaking the problems into smaller and smaller problems I was able to figure out the main issue. My biggest lesson from this frustration is to not update any package if you do not absolutely need it. Now, I'm a set back for this mistake and I need to update all the breaking changes in the form component.
