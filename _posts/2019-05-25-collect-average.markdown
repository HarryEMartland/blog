---
layout: post
title:  "Java Average of List"
date:   2019-05-25 15:18:50 +0100
permalink: /java-collect-average/
categories: spring-boot
tags: [java]
---

Don't reinvent the wheel! 
It is drilled into you when you are learning to code, but how do you know when you are?
If you are doing something which is pretty trivial or a common task, chances are it can either be done simpler or someone has done it for you.
I see developers often complicating things partly due to lack of experience but also people get a kick out of doing it themselves.

The most recent case of this for me was someone trying to get calculate the average, min and max of a list.
Straight away they started writing a loop, calculating the sum then the average.
After a bit of googling it turns out stream has a collector for this.

Here is a simplified version of the final code.
```java
Point location = new Point(3,2);
List<Point> points = Arrays.asList(
        new Point(1, 3), 
        new Point(3,5), 
        new Point(5,1));

DoubleSummaryStatistics statistics = points.stream()
    .collect(Collectors.summarizingDouble(point -> point.distance(location)));

LOG.debug("Avg: {}, Min: {}, Max: {}", 
    statistics.getAverage(), 
    statistics.getMin(), 
    statistics.getMax());
```