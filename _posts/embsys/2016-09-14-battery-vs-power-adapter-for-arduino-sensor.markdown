---
author: agarwali
comments: true
date: 2016-09-14 18:26:18+00:00
layout: post
title: Battery vs. Power adapter for Arduino sensor
meta:
category: embsys
excerpt_separator: <!--more-->
media:
media_source:
---

_In our Embedded systems class, we are designing and manufacturing Temperature and Humidity sensors (TH Sensor) for Pine Mountain Settlement School (PMSS) . After a group of students investigated the site for potential clues about how to go about designing the sensor, we are faced with an interesting challenge. How should we power our sensor? Batteries or Power Adapters? What kind of network communication links should we use? WiFi or Radio Links? Since there are many possibilities and challenges we came up with a conjecture: "Designing the sensor for battery and wifi is the simplest most direct pathway to solving PMSS SC."_

<!--more-->

### TL;DR


In this blog post, I will explore different sources that can be used to power our TH Sensors ( Arduino) and different communication links to for the TH Sensor to communicate data, and compare the advantages and disadvantages of using each of those sources.

**Note:** My comparisons are under the assumption that we will be using an Arduino as a platform for these TH Sensors.<!-- more -->


## Battery vs. Power Adapter


When it comes to powering a stand-alone Arduino (and "things" attached to it), we are presented with multiple options. We can use a wall power adapter, Alkaline batteries, NiMh batteries (rechargeable), LiPo batteries, Lead-Acid batteries.

![](https://images-na.ssl-images-amazon.com/images/I/61PE0FcaC4L._SL1001_.jpg)  ![Fig5](http://www.open-electronics.org/wp-content/uploads/2015/07/Fig5-500x375.png)


### Meeting requirements for client


In the case of PMSS, there are a couple of factors we need to keep in mind before we choose our power source.




  1. Most of these TH Sensors have to be very portable (e.g. they can be attached to the ceiling or walls).


  2. Aesthetics are important in certain places (so we do not want to see wire connections running down at some places).


  3. Some TH Sensors need to be installed in places where it usually out of reach.


  4. The TH Sensors will have to be always in an active state and report out data at intervals.


Considering these factors we can easily eliminate the big bulky Lead-Acid battery, which is definitely not portable. Even though Lead-Acid batteries can power our TH Sensors for a longer time than other batteries (has higher mAh) but it is also costly (~$20.00) and requires us to take extra measures to store the battery.

LiPo batteries are great to provide a high inrush of current, but the TH Sensor has to be always active, which means the batteries also has to be charged constantly. Under these conditions, the LiPo batteries would be damaged easily.


### Power Consumption


When designing an embedded system it is critical to choose a source that will meet the power consumption. With some initial research, I found that a typical Arduino allows 50mA of power when not used with any other sensors or LED. Assuming that we would use one LED as our indicator and a temperature and humidity sensor, everything combined would be drawing ~100 mA current per hour.

If we were to use alkaline batteries we would have to 4 of them in series to generate 6V to at least meet the voltage requirement for the Arduino. But we know that connecting batteries in series do not increase the current in the circuit. So we would get ~1500mAh power from our combination of 4 Alkaline batteries in series. If our TH Sensor draws 100 mA current per hour then the batteries would only last for 1500/100 = 15 hours. One solution to this problem is to use rechargeable NiMh batteries. But this would also mean that wee would have to recharge our battery every 15 hours (considering each NiMh battery provide 1500 mAh power). Now, we would need backup batteries since the TH Sensors have to be always kept alive.

Another factor we have not considered while talking about power consumption is that most TH Sensor will be placed on ceilings and walls that would not be regularly in the users reach. So it would be very difficult for the user to replace and keep track of so many sensors to replace the battery for recharge. Of course, we can build a circuit to recharge the battery from a power source, but then one can as the most obvious question, why not use the wall power source to power our TH Sensor directly?


### Costs


The cost of the power source is another important factor. A power adapter that connects to JAPAN Jack pin on Arduino Board costs approximately [$6.00](https://www.amazon.com/ZJchao-Power-Adapter-Arduino-2-Flat-Pin/dp/B00CP1QLSC) on Amazon. And a pack of 4 NiMh batteries costs approximately [$10.00](https://www.amazon.com/Westinghouse-NI-MH-2000MAH-Rechargeable-Batteries/dp/B00F2QMKB4/ref=sr_1_1?s=electronics&ie=UTF8&qid=1473875370&sr=1-1&keywords=nickle+metal+hydride+batteries). Even when considering costs, batteries are not the optimal choice.

So considering all these factors, I think power adapters are a better choice to power our TH Sensors.


## Bluetooth vs Wi-Fi


Sending and receiving data will be a big part of our TH Sensors, since it has to report out data to the user periodically. Given that PMSS do not have good Wi-Fi communication at certain points, I think we need to design a central system that communicates to the user over Wi-Fi through the internet. While other sensors, can report data to the central system using Bluetooth. Now, this could vary depending on how further apart are each building from one another.
