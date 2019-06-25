---
layout: post
title:  "Steps to Resilience"
date:   2019-06-25 00:00:00 +0100
categories: resilience
permalink: /steps-to-resilience/
tags: [resilience]
description: When making an application/service resilient what should you think about and in what order.
---

Often I see developers rushing into 'adding resilience' to applications without thinking about some of the fundamentals.
I have put this list together to try help guide people to build resilient applications correctly and by adding the right amount of resilience.
Don't just implement the cool new circuit breaker technology without doing the basics first!

1. Fallbacks
1. Timeouts
1. Monitoring
1. Alerting
1. Asynchronous
1. Circuit Breakers
1. Health checks
1. Highly Available
1. Auto-scaling

## Fallbacks
You should always be thinking about what to do if something goes wrong.
Sometimes it is fine to let default handles deal with an error but often it is better to do something.
If the system is not able to recover from an error you should at least think about warning the customer in a friendly way.
Some errors may be caused by optional components you should think about returning defaults and continuing to process in this situation.
Fallbacks will be used by other components of resilience.

## Timeouts
If you call is over a network such as an HTTP request or a DB call it is best to add a timeout.
Networks are inherently unstable and you should programme in a way expecting them to go down.
One of the worst failure modes is when a request takes an extremely long time.
Often in this scenario, all the threads of an application will get consumed or pools will be blocked upon.
Depending on your application all requests may start to error when only a small subset are having issues.
This issue can easily be fixed by adding a timeout to requests.
Most library's support a timeout but sadly often their default is infinite.
Try to set the time out as small as you can so if an issue occurs customers are not affected too much.

## Monitoring
It is great that your application is 'resilient' but it is important to be able to recover from issues.
In a perfect system, applications will self recover but in practice generally, something needs to be done.
To help figure out what has gone wrong and needs fixing applications should output errors in their logs and also expose metrics.
Dashboards can now be built to help visualise the metrics, spot anomaly's and figure out route causes.

## Alerting
Now your application is exposing metrics and you have some pretty dashboards are you going to employ someone to stare at them all day.
I hope your answer was no.
Tools are available to send notifications when your metrics behave in a certain way.
For example, you could write an alert when a services response time goes over 1 second.
Adding alerts means developers can spend more time developing and less time looking at graphs.
It also allows for out of hours to support to get on with their lives and only have to respond to issues.

## Asynchronous
Do you care about the result of all your API calls? Can a customer find out the result at a later date?
By taking things out of the main process it allows you to use systems such as queues.
Most queues have the functionality of retrying failed messages allowing you more chance for success.
Queues also can flatten out bursts in traffic which would normally cause issues.
If you don't care about the result of something then doing it asynchronously will stop any errors reaching the customer.

## Circuit Breakers
Circuit Breakers are a tool which stops your application sending requests to downstream services if the downstream service is struggling.
For example, the GitHub API your service uses is timing out. 
You have set a time out for 300ms, and your API calls GitHub 4 times per request but your service still brings value back without GitHub.
Your request is now taking 1.2s and customers are not happy.
A Circuit Breaker will monitor how often a request fails and if it passes a threshold will stop sending requests.
With a circuit breaker, your customers will only miss out on the functionality with issues.
The Circuit Breaker will periodically allow a request to go to the service and if successful allow requests again.

## Health checks
A health check allows you to quickly check if a service is running correctly.
Often implemented as a simple HTTP request which returns JSON showing the health status.
The health check should verify all the things needed by the service are accessible such as a database.
You need to be really careful about cascading failures due to a health check which depends on the health of a downstream service. 
It is best to just check that a downstream service is accessible rather than if it is healthy.
Can your application still run if it cannot access something?
If so it probably should not be in its health check.
An example might be an application which only periodically loads data in from a database.
If the database is down the service can still serve data all be it potentially stale data.

## Highly Available
Servers occasionally fail.
Racks and data-centres occasionally fail.
This could be due to hardware software or even accidents by humans.
Whatever the issue you want your service to be available.
Having a number of instances of your application running in different places gives you this protection.
You can make this as extreme as you like just having multiple instances, running in multiple data-centres and even running in different countries.
The important bit is having a load balancer which directs traffic to instances of your application which are healthy.
When an instance becomes unhealthy the load balancer should stop sending traffic to it.


## Auto-scaling
Your application is taking off and more and more customers are using it.
You also notice that at night your customers aren't using your application and your servers are sitting idle.
Auto-scaling allows you to add and remove servers to a pool allowing you to serve more customers when you need to.
Scaling down also limits the cost of servers when you don't need them.
You might not be able to predict when customers are going to start using your application.
There may be an advert on TV which causes a rush of users.
Having auto-scaling allows your application to react to customer demand and provide a good customer experience.