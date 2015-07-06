---
layout: post
title: Learning like a 5yo about managing servers
---

I think writing software is fun. Less fun is stressing out when the servers running your code crap out. As tech teams go, my compatriots and I are more app developers than tech ops/dev ops/whatever. Our first several months of running a site were more eventful than I was hoping.

First, there was a [huge AWS outage in June](http://aws.amazon.com/message/67457/) that took out both our app servers and our database servers several days before our launch date. On our launch date, we roundhouse kicked our own site when we reacted to high traffic by spinning up too many app servers and [accidentally overloading the number of available database connections](http://www.postgresql.org/docs/current/static/runtime-config-connection.html#GUC-MAX-CONNECTIONS)... we now know better. Excitement of this sort continued for a few months as we continued to have site issues almost every week.

A few doozies were particularly memorable.

One night during what should have been a routine deployment, I ran an upgrade script to change the database from version 23 to 24. Then I tried to deploy new app code, but the app servers failed to start because of inconsistent database version, and that was a non-starter for a website built on the Play 1.2 framework. That’s funny, how could that possibly be? I double-checked that the database schema was the correct version, and yet the app servers failed to start several more times. Meanwhile, our site is down and I start to hyperventilate because I feel crazy. I down a bottle of pinot noir to stave off a heart attack. Eventually, I noticed that the database’s load balancer incorrectly reported version 23 while the database itself was on version 24.

So replication was broken!! [Our database load balancer](http://www.pgpool.net/mediawiki/index.php/Main_Page) diverts many SELECT queries to the replica, which was still a version behind, and that incorrect version was what the application read. To fix the site, I pointed the application directly at the master database instead of at the load balancer, thereby cutting the replica out of the picture. And we ran our site directly on the master database for the next few days until we fixed replication. The whole ordeal probably lasted less than an hour, but time slows down to make it feel much longer. I swore to never write non-backward-compatible schema changes no matter how trivial a column rename feels, and to always keep a bottle of pinot on hand.

Doozy #2 is a story from a day when MLB sent emails to millions of baseball fans on our behalf. It was to be our highest traffic day yet, and [it went a bit like this](http://developer-blog.cloudbees.com/2013/01/play-framwork-our-most-popular.html) except that our site was much less prepared. In the earlier part of the day some visitors to our site were experiencing half-minute page loads omgz =(. It turned out that a CSS styles file was often taking a long time to download even though we had just started using [Amazon’s Cloudfront CDN](http://aws.amazon.com/cloudfront/) to serve that file, implying that Cloudfront was making roundtrips to the application server. We increased the cache period of that asset on Cloudfront, and that little change got our site back to loading pages within a second even under load! Actually it was our friends at [CloudBees](https://www.cloudbees.com/), our app server PaaS vendor, who made that observation.

And there are more stories like that chronicled in wiki pages that we write about each site incident.

Learning occurred, to say the least. But probably the most valuable thing I learned was not any technical kernel of knowledge but rather how to not freak out about site issues. They’re going to happen when you run a web business. The key is to chill out and use them as training moments, especially while our site is still young.

Despite all of this, I’ve calculated out that we maintained >99.98% uptime. Not bad for a few app developers, if I do say so myself.