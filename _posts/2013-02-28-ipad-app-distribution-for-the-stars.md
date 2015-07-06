---
layout: post
title: iPad app distribution for the stars
---

Celebrities on Egraphs use a [special iPad app to connect with their fans](https://www.youtube.com/watch?v=BfU_cE6HxDw). We didn’t want to put this app on the Apple app store because it is not meant for general usage, and also because we wanted to distribute upgrades without going through Apple. For us, security is crucial because much of the value of an egraph is its authenticity.

The recipe is actually quite simple.

Step 1 is initial distribution via email: To get the initial app to the iPad, we send an email to the celebrity with a link that installs the the initial version using the itms-services protocol.

Step 2 is to install the actual app via authenticated requests: When the celebrity logs into the initial app with a pre-provisioned account and password, that kicks off the process to download the actual app. The iPad makes a request to an egraphs.com server to get the locations of the .plist and .ipa files of the latest Egraphs iPad app. The .ipa lives privately on Amazon’s S3 and is only accessible through a [short-lived authenticated REST request generated by the server](http://s3.amazonaws.com/doc/s3-developer-guide/RESTAuthentication.html).

Step 3 is to enable easy app upgrades: To distribute updates of the Egraphs ipad app, we just update the .ipa URL on our servers. The next time a celebrity user logs into he iPad app, step 2 will kick off again and encourage the celebrity to allow the upgrade.

The problem of controlling distribution to iPad apps actually reminds me of what enterprises do with custom Box apps (I used to work at Box). I like to describe our iPad app distribution system as an enterprise-grade solution for your favorite celebrities.
