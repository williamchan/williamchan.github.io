---
layout: post
title: Mongo+Kerberos - documentation matters
---

By far the most painful work project of this year has been connecting the Paxata application to a Kerberos-protected Mongo database. I have come to the conclusion that if Kerberos is involved, then prepare for suffering.

I wish that the moral of this story was that I never give up on a technical challenge, but really I was saved by the patience of some really awesome people at Mongo. 

[Kerberos](https://en.wikipedia.org/wiki/Kerberos_(protocol)) is an authentication protocol that uses private keys, aka shared secrets, to secure computing resources and services. Shared secrets are really great for securing things, but in many cases, securely distributing those secrets is a showstopper because of the risk that those secrets are unsecurely transmitted. In a Kerberos environment, a trusted administrator configures those shared secrets within a closed computer network. (Think VP of IT at a large corporation.)

My devops coworker and I started work on this project by setting up a Mongo Enterprise server with a Kerberos client. Then the headwalling began as we tried unsuccessfully to connect to Kerberos-enabled Mongo from a command line. For 2-3 weeks, we double-checked the available documentation, puzzled over cryptic error messages, and exhaustively tested hypotheses. It wore me out to the point that I focused on other projects at work for a while.

I reengaged a few weeks later when I attended a [fascinating talk about Mongo version 3.0](http://www.meetup.com/San-Francisco-MongoDB-User-Group/events/220789385/) that touched on details about the inner workings of databases and distributed computing. From there, I connected with a Kerberos expert at Mongo who was willing to provide back-and-forth email support until I succeeded.

There were two major issues. The first, which had to do with logging into a Kerberos-enabled Mongo from a command line, ended up being a case where the documented example showed an incorrect approach. The second major hurdle encountered was that the Paxata application would not connect to that same database. The issue here ended up being... drumroll... quotations ("yes" "these" "things") around some [JAAS configs](https://en.wikipedia.org/wiki/Java_Authentication_and_Authorization_Service). Amount of illustrative documentation on the internet = zero.

So we can release a product to on-prem customers with confidence that they can use it with Kerberos-protected Mongo databases. I will prepare some documentation on how to set this up end-to-end.

And maybe someday I can get back to work that looks more like computer science. :)