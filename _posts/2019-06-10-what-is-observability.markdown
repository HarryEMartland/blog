---
layout: post
title:  "What is Observability? Real peoples thoughts"
date:   2019-06-27 00:00:00 +0100
categories: observability
permalink: /what-is-observability/
tags: [observability]
description: A collection of quotes to help highlight the different opinions of what Observability is.
---

Lots of people have tried to define what `Observability` is, this is not going to be another blog post trying to do this.
Instead this is going to be a collection of definitions from different people to try to let you make up your own mind.
This started as a presentation to the Observability Gild I gave when starting the guild but and thought it would be worth sharing.
Included are comments from myself and other people who viewed the presentation.


>In control theory, observability is a measure of how well internal states of a system can be inferred from knowledge of its external outputs.

_[Wikipedia](https://wikipedia.org/wiki/Observability)_

Observability is about making the internal state visible, as an example exposing JVM metrics through prometheus.
The prometheus metrics are externally accessible and without them you would not be able to see what is going on in the JVM.
It talks about a measurement as in there is a scale of observability it is not just all or nothing.

>Capable of being or liable to be observed; noticeable; visible; discernible:

_[Dictionary.com](https://dictionary.com/browse/observability)_

Just because your application is observable does not mean anyone is looking.
Observability is not a requirement for your application to run however when something goes wrong or needs investigating you start to care.

>Worthy or important enough to be celebrated, followed, or observed:

>Deserving of attention; noteworthy.

_[Dictionary.com](https://dictionary.com/browse/observability)_

If your service is important then it is important enough to be observed.
You should probably start collecting metrics from key services constantly.

>Observability is the extent to which the walls of a system have been made transparent

_David Duke (BookingGo - Test Lead)_

Again looking at internals of a system from the outside which are normally opaque walls.
Also you might have a system with walls which you can only see though parts we should aim for full transparency.
This definition also talks about a system rather than an application.
Your observability should encompass more than just the application and think about the whole system.

>The tools that we use to tell us what is going on within our microservices and between our microservices so that we can operate them effectively.

_[Colin Break (QCon 19)](https://www.infoq.com/presentations/challenges-operationalizing-microservices/)_

This definition talks more about the tools to make your application observable.
From what I have seen the tools are not the issue it is more about getting developers in the mindset and using the tools.
Again it is not just about the one application it is also about in between or how services communicate.
This is a great talk click the link above to watch it.
This is the firs definition to include why we want observability in that it helps us improve.

>Monitoring tells you whether a system is working, observability lets you ask why it isn't working.

_[VividCortext](https://vividcortex.com/blog/monitoring-isnt-observability)_

Often people are confused with Monitoring and Observability, this definition tries to clear it up.
When your application is observable you may have more information than you require but you know it may help in the future.
Observability is about preparing for the future where as monitoring is more about requirements of your application.
The value of observability is made clear when things go wrong and you can use it to figure out the route cause.

>"Observability", according to {a twitter blog post}, is a superset of “monitoring”, providing certain benefits and insights that “monitoring” tools come a cropper at.

_[@copyconstruct](medium.com/@copyconstruct/monitoring-and-observability-8417d1952e1c)_

Again comparing observability to monitoring saying of your application is observable then you must be monitoring.
This definition also mentions observability is more valuable than just monitoring.
Tools again are an important part of observability, if you are trying to do it from scratch you are probably doing it wrong.

>It can be tempting to combine monitoring with other aspects of inspecting systems, debugging, tracking exceptions or crashes, load testing, log collection, or traffic inspection. While most of these subjects share commonalities with basic monitoring, blending together too many results in overly complex and fragile systems.

_[Google SRE Book](https://landing.google.com/sre/sre-book/toc/index.html)_

The google SRE book is a great read if you are interested in Observability and Reliability.
This definition is more about monitoring saying don't do too much, you want a core set of metrics you trust to use.
If the thinks mentioned are not part of monitoring then I don't think they are part of observability either.

>Let me start with what I think observability is not: Observability is not a dashboard, it's not an alert that tells you your CPU has increased. Observability isn't a single activity you do before or after a release, and it's not a tool that you use to debug a particular fault. Observability is a feature of your system, its a culture you adopt.

_Emma Preston (BookingGo - Principal Test Engineer)_

People often think of observability as something you can just add once to your application and you are done.
This definition is saying it is more about the people using the application and how they can and do respond to incidents.
Culture is hard to change which is why observability is hard to introduce and maintain.

>Monitoring tackles what, practicing Observability exposes why. Monitoring is a verb, something that we do; Observability is a skill, something that we will hopefully possess with time

_Tom Riley (BookingGo - Senior Infrastructure Engineer)_

Observability is about the people and a skill they have.
Again this definition is differentiating monitoring and observability.
There is a long way to go in the observability space, lots of things to learn and improve.

>Its just a buzz word that we can use to build a better culture and toolset around monitoring in BookingGo

_Tom Riley (BookingGo - Senior Infrastructure Engineer)_

Product teams often forget about monitoring let alone observability.
If we can come up with a buzz word which gets people excited and actually monitor and care about their applications then that is great!
