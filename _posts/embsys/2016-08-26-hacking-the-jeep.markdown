---
author: agarwali
comments: true
date: 2016-08-26 16:34:27+00:00
layout: post
title: Hacking the Jeep
meta:
category: embsys
excerpt_separator: <!--more-->
media:
media_source: 
---

I was not surprised to see [the video](https://www.youtube.com/watch?v=MK0SrxBC1xs) where two hackers Charlie and Chris remotely hijacked an SUV. In fact, I had seen many similar videos. But what stood out to me most was the vulnerability of our software resulting in life-threating situations like having a jeep hacked in the middle of the highway while you are driving. 

<!--more-->

### TL;DR




### _Can we know if our Jeep was hacked and the brakes were modified to behave less accurately? _


My immediate answer is that we would never know if a jeep were hacked such that it does not behave accurately as it was intended to be. Before all the electronics and embedded systems came into play most machinery were controlled mechanically and obeyed laws of physics. The brakes were triggered by physical contacts and the driver would be able to sense the result of the trigger. Take a bicycle for example. If one pulls the brake, they can see the physical movements of wires and springs that eventually cause the bike to slow down. But with the use of embedded systems the driver can precisely reduce the speed of the car at a desired rate of deceleration almost instantaneously. As a result, we do not see or feel the change in the physical state of the machine. The results or deceleration, which is the reduction of speed is displayed on a digital display which is also vulnerable to attacks as seen in the video. So, if the brakes were hacked such that they behave less accurately the driver will not be able to sense it until he has been pressing the brakes for a long time and he does not feel the car is slowing down, which is certainly not the case in an emergency situation.


### _ What implications do "smart cars" have for forensics and crash investigations, and do you believe we have the tools to handle such investigations today? _


Smart Cars are definitely at a higher risk of cyber attacks or crimes making forensics and crash investigation more difficult than ever. One key indicator is the comparison of market growth between smart electronic devices and cyber security. According to the [cyber security market report](http://cybersecurityventures.com/cybersecurity-market-report/), the rate of growth of market size for electronic devices such as PCs, tablets, smartphones, and Internet of Things(IoT) devices has superseded the rate of growth of market size for cyber security. I believe that due to increased demand in smart electronic products companies are not taking the time to invest in or simply do not have enough resources to invest in securing their products from potential cyber attacks. Some of those security measures include tools that will help in tracing attackers when they intervene the system. I think that we have the tools and the intelligence to be able to perform criminal investigation but the producers of smart cars are not making the effort to put them in place.


### **_After graduating from Berea College will I be ready to work on life-critical software and embedded systems?_**


After graduating from Berea College, I believe I will have enough knowledge and confidence to start working with life-critical software and embedded systems. Some of the most important courses other than the core courses at Berea would be Software Engineering,  where I learned how to work with a large codebase and a similarly large community. The course Electricity and Electronics provided a good introduction to the world of electronics, but with Embedded Systems I expect to gain a deeper understanding of electronics and IoTs. On the other hand, the course Computer Security is another essential course that would help me built critical systems that are less susceptible to foreign attacks. However, I believe, that courses alone would not be sufficient. I will need to have worked on personal projects and done internships to connect concepts learned in classes to real world problems.


### _**What practices with regards to the writing of code and working in teams will be crucial?**_


In terms of writing code, it is essential to learn the best practices and conventions. One should also learn how to document the code properly so that other programmers are able to understand how the program works. It is also important to thoroughly test the intended purpose of a program, so that the users are satisfied and hackers cannot take unfair advantage of the loopholes in the program, like the hijacking the jeep video. On the other hand, learning how to work in teams is really important as I can speak from my summer experience at Interapt. To ensure that team is productive everyone has to communicate well their problems as well as discoveries especially in the case of developing life-critical software where a miscommunication can cause hazards.


### _**List of strategies and practices that are employed by practitioners in industry to develop reliable, safe software for embedded systems.**_


In the article "_[Five Steps to Improving Security in Embedded Systems](http://www.newelectronics.co.uk/article-images/46294%5CFive%20steps%20to%20improving%20security%20in%20Embedded%20Systems.pdf)"_,  the author talks about five high-level security that embedded system designers should consider.




  1. Conduct an End-to-End Threat Assessment - performing tests on the systems will real-life situations that might cause security issues.


  2. Leverage Existing Advanced Security Designs


  3. Select an Appropriate Run-Time Platform


  4. Secure the Applications


  5. Adopt Comprehensive Life Cycle Support
