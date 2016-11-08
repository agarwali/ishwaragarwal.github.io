---
author: agarwali
comments: true
date: 2016-10-07 05:18:05+00:00
layout: post
title: Using Arduino Pro Mini as a low power consuming platform
meta:
category: embedded-systems
excerpt_separator: <!--more-->
media:
media_source:
---

_I'm almost midway in my embedded system course where, as a class, we are designing temperature and humidity sensor(THS) for Pine Mountain Settlement School(PMSS). Last week, we had the opportunity to meet Geoff, executive director of PMSS, and ask various questions to deconstruct all the ideas to build this THS._ <!--more-->_One of the things that we discovered during this process was THS has to be battery powered and the battery has to survive at least six months before replacement. This led us to explore this interesting question: How can we design a THS that runs on battery(cell) for at least six months?_

### TL;DR

In this blog, I'm going to write about an option we are exploring to build low powered temperature and humidity sensor with Arduino Pro Mini.


### Modyfying Arduino Pro Mini


The main reason we chose to use Arduino Pro Mini rather than building our own platform is becuase only have half of this Fall 2016 semester left to deliver this sensors. It is not worth our time diving into the wilderness of building a platform and make mistakes, which is ofcourse unavoidable. In the blog "[Arduino Low Power - How to run ATMEGA328p for a year on coin cell battery](http://www.home-automation-community.com/arduino-low-power-how-to-run-atmega328p-for-a-year-on-coin-cell-battery/)", the author discusses some strategies where we run ATMEGA328p on an coin cell for a year on a Arduino Pro Mini platform. An unmodified Arduino Pro Mini can comsume upto 45 mA current which will consume 9A battery in less than a day. However, with simple modification we can signifiicantly reduce that amount of current consumed upto 0.0045 mA.  The power LED and Regulator are the two components asides the microcontroller that consumes a lot of current on Ardunio Pro Mini. Below is a table provided by the author of the blog that shows current consumption for different combinations of modified and unmodified versions of Arduino Pro Mini with ATMega328p.
<table >

<tr >
ATmega328P Pro Mini Version
PWR Source
State
5.0 V @ 16 MHz
3.3 V @ 8 MHz
</tr>

<tbody >
<tr >

<td >Unmodified
</td>

<td >RAW Pin
</td>

<td >ACT
</td>

<td >19.9 mA
</td>

<td >4.74 mA
</td>
</tr>
<tr >

<td >Unmodified
</td>

<td >RAW Pin
</td>

<td >PDS
</td>

<td >3.14 mA
</td>

<td >0.90 mA
</td>
</tr>
<tr >

<td >No Power LED
</td>

<td >RAW Pin
</td>

<td >ACT
</td>

<td >16.9 mA
</td>

<td >3.90 mA
</td>
</tr>
<tr >

<td >No Power LED
</td>

<td >RAW Pin
</td>

<td >PDS
</td>

<td >0.0232 mA*
</td>

<td >0.0541 mA*
</td>
</tr>
<tr >

<td >No Power LED, no Regulator
</td>

<td >VCC Pin
</td>

<td >ACT
</td>

<td >12.7 mA
</td>

<td >3.58 mA
</td>
</tr>
<tr >

<td >No Power LED, no Regulator
</td>

<td >VCC Pin
</td>

<td >PDS
</td>

<td >0.0058 mA
</td>

<td >0.0045 mA
</td>
</tr>
</tbody>
</table>


In addition to modifying the Arduino board, we have to be able to make the processor go to sleep. The ATMega328p supports a number of sleep modes and peripherals that can be controlled using external libraries. We will be using the [RocketStream](https://github.com/rocketscream/Low-Power) library to turn the Arduino to sleep.


### Next Steps


The next steps for my power management team is to experiemnt with ATMega328p and Arduino Pro Mini. Ideally, we would like to have the Arduino Pro Mini board soldered and setup and run the BlinkLight example code.

In addtition, I will be travelling to PMSS this weekend with my group to complete building and deploying our first prototype of Temperature and Humidity Sensor on a RaspberryPi. So, next week I will be blogging a reflection on our work done at PMSS.
