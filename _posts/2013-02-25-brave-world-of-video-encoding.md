---
layout: post
title: The brave world of video encoding
---

One of my recent projects was to build the new egraph page. As explained in a company blog post, the new format delivers the egraph’s audio and image together as a video, versus as separate image and audio assets.

Much of the motivation for this exploration was that we figured out that many people who viewed egraphs completely missed that there is an audio experience. By presenting the egraph as a video with a BAPB (big ass play button), we hope that it is obvious to egraph viewers that there is something to experience by hitting the play button. Hear your star speak directly to you omgz.

Enter the brave world of video encoding. As this as my first foray into that world, I was in for a crash source. For starters, there are currently three major codecs. As [Dive Into Html 5](http://diveintohtml5.info/video.html) recommends for maximum compatibility, a website should provide a video in all three formats as well as a flash fallback. So much for hoping that video would be a limited scope problem.

And secondly, even combining a single image with an audio track turned out to be more difficult than I initially anticipated. Major open-source video libraries like FFmpeg run on native code, and all of my encoding attempts involved using a Java library called Xuggle, which wraps FFmpeg. I found Xuggle to be extremely finicky, and given how frequently that library is referenced, I would say that the JVM world does not have great video support.

I managed to create an MP4 from egraph assets, and those MP4s were what I shipped out the door. Currently, the egraph page displays the MP4 with flash fallback provided by [Video JS (Zencoder)](http://www.videojs.com/) in a single resolution. We shipped it because, judging from the browsers they use, a very small percentage of our users would not be able to play the video, and besides our beautiful classic egraph view is still available. But if time and money were unlimited, video encoding is clearly a project we can spend more time on.

Complexity in video encoding is introduced on one axis by the competing video formats, on a second axis by the wide range of viewing devices that span iPhones, Android phones, browsers, tablets, and TVs, and on a third axis by the speed of the viewing device’s internet connection. Did you know that [Netflix encodes each video 120 times](https://gigaom.com/2012/12/18/netflix-encoding/) so that you can watch [Archer](http://www.amazon.com/Archer-Season-H-Jon-Benjamin/dp/B00475B0G2) wherever you want? And the next time I upload an arbitrary video to Youtube, I will admire the fact that it just works. For the rest of us who are not large tech companies, there are services like Zencoder and now Amazon Elastic Transcoder. I tip my hat to Zencoder for being ahead of the curve in recognizing the need for sophisticated video encoding services.

When [AWS introduced their service](https://aws.amazon.com/blogs/aws/amazon-elastic-transcoder/), they described that: ”Implementing a transcoding system on your own can be fairly complex. You might need to use a combination of open source and commercial code, and you’ll need to deal with scaling and storage…. In short, it isn’t as easy as it could be.” That sounds about right to me. :-)

But the deeper you explore hard problems, the more obvious business opportunities seem.
