---
layout: default
title: Types of Monitor Latency
parent: Monitor Latency Guide
nav_order: 1
---

# Types of Monitor Latency
{: .no_toc }

## On Display Latency

You can test this with:
### Dedicated Testers
Tools like the Leo Bodnar Latency tester, or the Time Sleuth output frames over HDMI, then wait to register the light level change. Since they know when they sent the frame, they can time how long it takes the monitor to process and draw the frame. These are great, but do come with some limitations. These are often based on an FPGA (field programmable gate array), specifically, low power FPGAs. The Time Sleuth caps out at 1080p60 output, which means for anything higher end than that, the monitor is going to have to translate that 1080p frame up to native resolution - which for a non-direct resolution like 1440p might add unrealistic latency. 

### OSLTT's new trick
The alternative is using a more complete system, but controlling each step in the event path so you can subtract out any time taken for USB polling and frame processing, leaving you with the on display latency. This is much more realistic as the graphics card will always output the target resolution, and is much closer to how an end user is using their system. The catch to this method is that because it's a computer generating new frames (at a constant rate) rather than a dedicated device which is able to time when a "target" frame leaves the device, this method has to wait for up to a full refresh rate cycle. Much like USB polling delay which can vary from 0.1 to 0.99 ms (at 1000Hz), on a 60Hz display the input latency may report as anything from 0.1 to 16.6 ms, and anywhere in between. Repeating this test will only get you an average of around half the refresh rate, so it's not quite as accurate as you might like. 

## Total System Latency
On the flip side, you can exclusively measure the full end user experience, what I call the "Total System Latency", or what Linus calls the "Click to Photon Latency". This is the ultimate real-world measure, as it's literally measuring what someone playing their favourite game will experience. This is really easy to measure, either with a high speed camera (1000FPS or higher ideally) and an LED attached to a mouse button, or with something like OSRTT or NVIDIA's LDAT tool. 

The major problem with this method though is that it isn't a good metric for reviewers to publish with, since it is so intrinsically tied to the system, game, and even in game events. A reviewer testing on a high end gaming PC with a top shelf CPU and GPU is likely to give much faster results than someone rocking a budget ebay dumpster-dive system, and even on the same system if you chose to test with CSGO you'll get one figure, but test with Cyberpunk 2077 and you'll get a very, very different result. Neither of those would have much of anything to do with the monitor. If you keep your test methodology perfectly consistent, then as a direct comparison to your other data, it can work - but it still isn't the best for monitor reviews.

## Comparative Method
Alternatively, you can use a monitor with a known latency as a point of comparison. This method is one Simon from TFT Central covers in depth in his guide you should [check out here](https://tftcentral.co.uk/articles/input_lag) but to summarise - if you know how long the input latency takes on a set monitor (possibly even a CRT display!), using a high speed timer duplicated on both displays you can take a picture of both screens and compare the timer figures. Subtracting the difference between the two and adding the known value back in gets you your result. This is a wild oversimplification so please do read Simon's excellent guide on the topic. 