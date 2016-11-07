---
author: agarwali
comments: true
date: 2016-06-17 01:56:56+00:00
layout: post
title: Authentication with Google in Angular 2
meta:
category: internship-2016
excerpt_separator: <!--more-->
media:
media_source:
tags:
- angular2
- authentication
- google
- signin
---


_This post is about creating sign-in and authentication with google API._

In Google Sign-In for Websites documentation, there is an option to create custom google sign-in button.

<!--more-->

To create a Google Sign-In button with custom settings, we have to add an element to contain the sign-in button to our sign-in page, then we write a function that calls[`signin2.render()`](https://developers.google.com/identity/sign-in/web/reference#gapi.signin2.render) . However, the button is not rendered dynamically in Angular 2.

So we will use ngAfterViewInit component lifecycle hook, that will call the [`signin2.render()`](https://developers.google.com/identity/sign-in/web/reference#gapi.signin2.render)function after the view is initialized in Angular 2.


    import {Component, NgZone} from '@angular/core';

    declare var gapi: any;

    @Component({
      selector: 'login',
      template: '





', }) export class LoginComponent { googleLoginButtonId = "google-login-button"; constructor( private _zone: NgZone) {} ngAfterViewInit() { // Converts the Google login button stub to an actual button. gapi.signin2.render( this.googleLoginButtonId, { 'onsuccess': this.onLoginInSuccess, 'onfailure': this.onLoginFailure, 'scope': 'profile', 'theme': 'light', 'width': 240, 'height': 50, }); } private onLoginInSuccess = (loggedInUser: any) => { this._zone.run(() => { var email = loggedInUser.getBasicProfile().getEmail(); var auth_token = loggedInUser.getAuthResponse().id_token; // Use a service to store authenticate with backend // Store token in local storage for authentication }); } private onLoginFailure = (error: any) => { console.log(error); } }

In the component above the onLoginSuccess method is called which has the loggedIUser parameter that we can use to get user information and authentication token. It is important to make use of an `NgZone` object to make sure that the property updates occur in a context of which Angular 2 is aware.
