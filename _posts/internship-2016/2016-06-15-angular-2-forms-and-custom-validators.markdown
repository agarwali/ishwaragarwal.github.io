---
author: agarwali
comments: true
date: 2016-06-15 04:55:34+00:00
layout: post
title: Angular 2 Forms and Custom Validators
meta:
category: internship-2016
excerpt_separator: <!--more-->
media:
media_source:
tags:
- angular2
- asynchronous
- custom
- forms
- synchronous
- validators
---

_This post will be about my reflection on Agular 2 forms, and creating custom synchronous and asynchronous validators._

Forms are the cornerstone of any web application. Angular 2 provides mainly two ways for creating forms, template-driven and model-driven.  In a template-driven form we use two-way data binding ,  `ngModel` and map to our internal data model. However, in a model -driven form we build our models and controls explicitly.

<!--more-->

For example here is a simple signup form:


    <span class="nt"><form</span> <span class="err">[</span><span class="na">ngFormModel</span><span class="err">]="signup</span><span class="na">Form</span><span class="err">"</span> <span class="err">(</span><span class="na">submit</span><span class="err">)="signup</span><span class="err">(</span><span class="err">)"</span><span class="nt">>
    </span><span class="nt">    <input</span> <span class="na">ngControl=</span><span class="s">"email"</span> <span class="na">type=</span><span class="s">"email"</span><span class="nt">>
    </span><span class="nt">    <input</span> <span class="na">ngControl=</span><span class="s">"password"</span> <span class="na">type=</span><span class="s">"password"</span><span class="nt">>
    </span><span class="nt">    <button</span> <span class="na">type=</span><span class="s">"submit"</span><span class="nt">>Sign Up</span><span class="nt"></button>
    </span><span class="nt"></form></span>


Here is the corresponding model-drivel form component.


    <span class="kr">import</span> <span class="p">{</span> <span class="nx">Component</span> <span class="p">}</span> <span class="nx">from</span> <span class="s1">'@angular/core'</span><span class="p">;
    </span><span class="kr">import</span> <span class="p">{</span> FormGroup, <span class="nx">FormBuilder</span><span class="p">,</span> <span class="nx">Validators</span> <span class="p">}</span> <span class="nx">from</span> <span class="s1">'@angular/forms'</span><span class="p">;

    </span><span class="err">@</span><span class="nx">Component</span><span class="p">({</span>
    <span class="na">    selector</span><span class="p">:</span> <span class="s1">'signup-page'</span><span class="p">,
    </span><span class="na">    templateUrl</span><span class="p">:</span> <span class="s1">'signup-page.html'
    </span><span class="p">})
    </span><span class="kr">export</span> <span class="kr">class</span> Signup<span class="nx">FormComponent</span> <span class="p">{
        private signupForm: FormGroup;
    </span><span class="nx">    constructor</span><span class="p">(</span><span class="nx">fb</span><span class="err">:</span> <span class="nx">FormBuilder</span><span class="p">)</span> <span class="p">{
    </span><span class="k">        this</span><span class="p">.signup</span><span class="nx">Form</span> <span class="o">=</span> <span class="nx">fb</span><span class="p">.</span><span class="nx">group</span><span class="p">({
    </span><span class="na">            email</span><span class="p">:</span> <span class="p">[</span><span class="s2">""</span><span class="p">,</span> <span class="nx">Validators</span><span class="p">.</span><span class="nx">required</span><span class="p">],
    </span><span class="na">            password</span><span class="p">:</span> <span class="p">[</span><span class="s2">""</span><span class="p">,</span> <span class="nx">Validators</span><span class="p">.</span><span class="nx">required</span><span class="p">]
    </span><span class="p">        });
    </span><span class="p">    }

    </span><span class="nx">    signup</span><span class="p">(</span><span class="p">)</span> <span class="p">{
    </span><span class="nx">        console</span><span class="p">.</span><span class="nx">log</span><span class="p">(</span><span class="k">this</span><span class="p">.signup</span><span class="nx">Form</span><span class="p">.</span><span class="nx">value</span><span class="p">);
    </span><span class="nx">        // in reality we would use a service to post the data to an api</span>
    <span class="p">    }
    </span><span class="p">}</span>


Form Builder is an easy way for us to create form controls and control groups. It allows us to specify what specific form validator(s) to be applied to a particular control object. In the example, we use the built-in required validator which will change the error property of the control object to true if the input field is unfilled. We can use this data to show error messages, and disable the submit button until the user enters the required information.

The advantage of using model-driven as opposed to template-driven forms in Angular 2 is the ability to provide custom created validators to the control object. For example, we might want to check if the password contains at least one special character and a number. This is a synchronous validator. But we can also create asynchronous validators in Angular 2 where we will request information from the server. For example, in the registration form, we might want to check that the username is unique during registration.


    import {FormControl} from '@angular/forms';

    export class UsernameValidators {
     static shouldBeUnique(control: FormControl) {
     var username = control.value;
     // send request to server to check if username is unique
     // return null; <-- if username is uniuqe
     // return {unique: true}; <-- if username is not unique  
     }
