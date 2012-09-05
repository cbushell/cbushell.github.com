---
layout: post
title: "Anti Patterns of Enterprise Application Architecture: The Database Application"
date: 2010-02-11 21:00
comments: true
categories: 
---

Most large enterprises enforce a gated deployment process to take an application from development to production. That’s to say that an application must pass through a number of different environments before it gets signed off to enter the production environment.

For example, an application developed on a desktop machine must first be deployed to a QA environment, then a UAT environment and maybe a Performance Testing environment before finally being given the OK to move to production, for the whole world to see.

This process usually requires sign off from at least one manager, probably more. Coupled with the fact that corporate IT departments are often divided into areas of functional responsibility (think database, application server, security etc.), and moving the various components of an application through each environment requires the co-ordination of several different teams. The result is that taking an application to production is not a quick process, and usually ends up taking several days, if not weeks.

Business sponsors of IT projects end up feeling frustrated by how long it takes to make even minor changes to the applications that they pay for, and developers are left feeling like they’re letting their sponsors down.

The path of least resistance to deploying anything to the production environment often emerges as the database. After all, that’s only a single layer of your application, right? So, the process of moving database changes to production avoids the need to co-ordinate several different teams and deal with complications arising from error prone application server deployments, and other potential points of failure.

The path of least resistance to deploying anything to the production environment often emerges as the database. After all, that’s only a single layer of your application, right? So, the process of moving database changes to production avoids the need to co-ordinate several different teams and deal with complications arising from error prone application server deployments, and other potential points of failure.

What people often over look is that the more and more configuration you push into the database, the more and more the application you’re developing starts to resemble an interpreter. It becomes possible to configure virtually every feature your application has to offer from the database. At this point your application starts becoming the equivalent of the JVM or .Net run-time, and the database is really just a glorified source code repository playing host to the code that your application interprets at run-time.

Take it a step further, and why not move some of the logic behind your application into the database. It’s amazing what you can do with a few thousands of lines of stored procedure code!

But have you ever tried to debug several thousand lines of stored procedure? I have, and I blame my thinning hairline on the experience.

And testing? Well, that just seems to get slowly forgotten. Given that we already know it’s so easy to make changes to the production database, so what if things go wrong in production. It’s easy enough to correct mistakes by pushing out another untested database change straight to production. A few hours (or maybe days) of downtime isn’t that bad, is it?

We’re all in agreement that separating application logic from configuration is a good thing that allows us to re-use code we’ve written, but let’s not take things too far. Of course, the ideal solution would be to change the process so that moving an application to production is quicker, but we’re rarely in a position to do this. Instead of trying to work around the corporate red tape that makes it difficult to deploy changes to production, the best we can do in this situation is to oil the gears that need to turn to get things done.

That faceless application server support guy you always email to get your application deployed to QA? Why not take him out to lunch and get to know him? The security guy you always email to get ports opened for your application to function correctly? How was his weekend? And how are his kids going at school? Pick up the phone and find out. You’ll be amazed how much more quickly you can get your application moved through different environments and to production when you have a relationship with the people you need to make it happen. Instead of compromising the quality of your application by pushing everything to the database, why not give it a try?
