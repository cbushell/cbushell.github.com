---
layout: post
title: "REST in Practice Tutorial"
date: 2010-11-28 21:01
comments: true
categories: 
---

I was fortunate enough to attend a [REST in Practice](http://oreilly.com/catalog/9780596805838/) tutorial run by [Jim Webber](http://jim.webber.name/) yesterday. The material was taken from the recently published book of the same name co-authored by [Savas Parastatidis](http://savas.me/) and [Ian Robinson](http://iansrobinson.com/).

As you might expect, the tutorial followed the contents of the book closely and used the [Richardson model](http://martinfowler.com/articles/richardsonMaturityModel.html) as it’s outline. The tone for the tutorial was set with a discussion about the state of most enterprise architectures today, covering the Richardson level 0 stuff. The conclusion was that most enterprise architectures go out of their way to hide the network from us, which has resulted in some very complex solutions to inherently difficult problems (scalability, distributed computing, error handling etc.). The result being even more complexity.

It turns out that [Tim Berners-Lee](http://www.w3.org/People/Berners-Lee/) solved a lot of these problems over 20 years ago when he designed the foundations of the web. Jim continued to explain the web as a platform, introducing resources, HTTP verbs and hypermedia/HATEOAS as we worked through Richardson levels 1-3. Along the way we covered content types, response codes, scalability, caching, ATOM and security.

I still haven’t read REST In Practice yet (it’s top of my reading list as I write this), but got a lot out of the tutorial – a lot of practical advice which I can take away and use immediately. Jim was as entertaining as always, and a great presenter (although a little disappointed at times when checking the cricket scores).

Jim’s running the tutorial with Ian as part of [YOW!2010](http://www.yowconference.com.au/) this week in Australia, and there have been [other dates globally](http://www.thoughtworks.com/rest-in-practice/). I’d highly recommend this tutorial for anyone working on distributed systems, in the enterprise or otherwise.
