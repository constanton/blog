---
title: "A simple demo on the impact of latency in teleoperation"
pubDate: "2016-09-12T07:49:39.000Z"
description: "A Chai3D haptics demo showing how network latency can destabilize remote control and force feedback."
---
Hello everyone!

It’s been so long since I wrote a blog post. You can’t imagine how much I’ve been waiting for a reason to start writing and…here it is!

Since the last time I wrote something, I finished with my MSc degree at NKUA and started my PhD at King’s College London. I am now studying and working on haptics over the upcoming 5G network infrastructure. How they work, how to improve it and how to make it more usable for a number of use cases are a few questions I’m looking to answer.

### The demo

I’m happy to say that I have just uploaded the first demo I ever made since I joined the KCL-Ericsson 5G lab. It’s rather simple but gets the job done. It also doesn’t fail to impress people who don’t know how it’s like to teleoperate something under latency.

So, here it is: [https://github.com/constanton/DelayedTeleoperationDemo](https://github.com/constanton/DelayedTeleoperationDemo)

It’s actually a modified version of one of the examples provided by the Chai3D C++ framework that I’ve been using lately. The modification was simply creating one buffer at the position channel and another one at the feedback channel. As you increase the latency (ie. the size of the buffers) above 10ms, the end result is the de-synchronization of the data you receive and the data you send making the haptic device to become unstable…it really starts to “kick” when you touch anything with the grey ball.

The haptic device used is the Sensable Phantom Omni (IEEE 1384 version) which works only under Windows (at least for me). So, in case anyone has made it work under Linux, if possible, please send over a how to 🙂

There is room for improvements, further modifications and optimizations. One idea is to implement at least one stability control algorithm to compare it to the usage without one.

Anyway, here is a pic from the application.

[Application screenshot (image unavailable)](http://localhost/wordpress/wp-content/uploads/2016/09/dtd.jpeg)

You can slide the cylinder along the string using the grey ball which you control from the haptic device. You can change the latency (bottom right) with + and – keys.
