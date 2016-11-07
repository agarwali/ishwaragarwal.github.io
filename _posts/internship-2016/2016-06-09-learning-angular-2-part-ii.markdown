---
author: agarwali
comments: true
date: 2016-06-09 17:58:59+00:00
layout: post
title: Learning Angular 2 Part II
meta:
category: internship-2016
excerpt_separator: <!--more-->
media:
media_source:
tags:
- angular2
---



_This is going to be my second post about Angular 2 following the first one I did last week. In this post, I'll discuss the basic building blocks of Angular 2 and how it's reusability has made developer's life easy. This will not be a documentation or tutorial for Angular 2, and there is no point in creating one as there are so many tutorials out there. It will be my reflection on what I've learn so far._

<!--more-->

In a nutshell, there are four key concepts in an Angular 2 app:




  1. Components


  2. Directives


  3. Routers


  4. Services




### Components


Components are the basic building blocks of an Angular 2 application. A component encapsulates a template, some data and the behaviour of a view. Every Angular 2 application has at least one component, the root component. In a real world application, there can be hundreds of components that control the behavior of a view.

Let's look at the home page of this blog as an example. There is a navbar, a sidebar,  a blogs area, a footer. Now the blogs area can be broken down into small blog excerpts component, and then each blog component can be further broken down into a text area component, and a social media sharing component. The idea here is to break down a large application with complex views into smaller and more manageable components that render a specific view. This increases the reusability of a component in the same application or a totally different application. For example, I can use the social media component in a totally different application.

So what does it actually look like in code. A component is basically a TypeScript class with methods and properties(attributes), just like any other class.  The properties hold the data for the view, while the methods control the behaviour for the view.


    export class AppComponent {
        title = "Hello";
        onClick() {
            // do something
        }
    }


Unlike JavaScript or  jQuery, the DOM is decoupled from the component, which makes the component unit-testable. Instead in the DOM, we bind to the properties or methods of our components using templating syntax.


    <h1>{{ title }}</h1>
    <button (click)="onClick()">Do Something</button>




### Directives


Similar to components directives modify the DOM elements by controlling its behaviour. Directives, unlike a component, does not have HTML markup associated with it. It is used to extend the behaviour of an existing view in a component. For example, we can use a directive on a button example above to float, when a user hovers on the button.


### Routers


Routers are used to control the routing between different views in our single page application. It allows us to specify how a user can change its views when they trigger some event. We can apply logic in our router such as authentication guards that will restrict users from an authorized access.


###  Services


Our application often needs to communicate with a server to GET or POST data. In Angular 2 we delegate this business logic to services instead of putting them in components. The components can subscribe to these services to get or post data. The services can be reused in other components as well.

This concludes my reflection on Angular 2 Part II. I'll be posting more reflections of different aspects of Angular 2 as I learn or apply them in my project.
