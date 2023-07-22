---
layout: default
title: Measuring Latency
parent: Input Latency Guide
nav_order: 3
---

# Measuring Latency
{: .no_toc }

## On Display Latency with OSRTT
I'll focus on how I am measuring latency here, rather than a more generic guide. Primarily, from a monitor perspective what I'm looking to measure how long it takes from the frame leaving the graphics card, to the frame starting to be drawn on screen. That includes processing the frame from a digital stream to a pixel array, which includes doing look ups and calculations for any overdrive modes and any post-processing effects too. Some monitors are pretty... lackadaisical. Most gaming monitors tend to be in the 1 to 2ms range generally. As always with latency, the lower the better, but anything under 5ms I'd personally call fine. 

To expand on the difficulty in measuring the latency when you can't control when the next frame is sent - for tools like the Time Sleuth, because the same chip that measures the timing is the one generating the new frame, it can very accurately tell how long the display took to start rendering that frame. On something like OSRTT though, because it's the GPU rendering new frames (regardless of new inputs), I can't precisely time when a new frame is generated in relation to the refresh window. If you were using a 60 Hz display, that means the display is drawing a new frame every 16.67ms. If OSRTT triggers a click event to the DirectX window right after a refresh, well at 1000FPS the new frame will be generated in just 1ms, but it's going to have to wait something like 15ms for the display to be ready to display that new frame. That adds potentially up to 16.5ms of latency to the result that otherwise wouldn't be there if you control when new frames leave the device. 

That isn't an ideal measurement obviously, but it is a real world measurement and it isn't affected by the same issues something like the Time Sleuth is where the monitor is the one doing the image scaling to the correct resolution. As long as none of the results are higher than the refresh rate window time, you know the input lag is not visible to the end user. 

## How it's calculated
For OSRTT, the process is pretty simple. The board records the time in microseconds, sends the mouse click (or actually with the new DirectX code it sends either "1" or "6" for better reliability), then records the time again which tells you how long the USB polling delay took. It then starts reading data from the ADC at around 55,000 samples per second (every 18.3us in the real world) for 200ms. That's just under 11,000 samples! Once that's done it records the time again to tell you exactly how long the sampling took, then it sends all that data over serial to the desktop app. The desktop app, which also recorded the frame time during the input event, then processes all those samples. It looks for the start point - when the data goes from a flat, low line, to when it sharply rises and works out how long that took. It can then subtract how long the frame took to render and that gives you the on display latency. 

## Why isn't the response time included?
This is a very valid question, and I wouldn't consider this a settled debate. I chose to not include it for a number of reasons I will list below. I'm very much open to discussion on this point though, so feel free to reach out if you'd like to add anything.
-   The test is to work out how long the monitor takes to process the frame, not how long it takes to draw it. We have the response time measurement for that.
-   When to consider the frame "drawn" is already a topic of debate on the response time measurements - is it when the frame is 100% fully drawn, including overshoot? Or when 90% of the initial transition is done? Or maybe 3% of the RGB range is left? 
-   From a technical standpoint, detecting the start of a large change (RGB 0 to RGB 255) is much easier and more reliable than detecting a potentially arbitrary end point to a messy transition. For the best repeatability and reliability using the start is much better.