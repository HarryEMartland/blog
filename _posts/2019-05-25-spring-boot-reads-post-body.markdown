---
layout: post
title:  "Spring Boot Reads Post Body"
date:   2019-05-25 15:18:50 +0100
categories: spring-boot
permalink: /spring-boot-post-body/
tags: [spring-boot, webflux, rx]
---

At work, we were presented with an interesting bug.
For background we essentially have a [Spring Boot Webflux](https://spring.io/guides/gs/reactive-rest-service/) app acting as kind of a reverse proxy.
The bug was we were receiving an HTTP 500 response for certain requests. 
Due to the complexity of the system, we were working on it took us a while to realise it was specifically `POST` requests.
`GET` requests where fine.

Webflux is reactive and the service was reading the whole body of the request.
To read the body you receive a [Mono](https://www.baeldung.com/reactor-core) which is an [observable object](http://reactivex.io/documentation/observable.html).
Observable objects can only be 'observed' once and we could see in the logs something was reading it for a second time.
We could only see our code reading it once so why would this be an issue?
Spoiler alert it's in the title.

It turns out that Spring is super helpful (not for us :/) and reads `application/x-www-form-urlencoded` `POST` requests into a handy map.
I get why Spring does this, my issue is that you cannot turn it off and the errors you receive are not super useful.
Spring Boot is convention over configuration but I think it is important that you can override the convention.
Our fix was to use the map spring creates rather than the body if the content type is `application/x-www-form-urlencoded` and proxy that on.