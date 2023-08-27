---
layout: default
title: Getting Started
nav_order: 3
---

# Getting Started
{: .no_toc }


Assuming you have an OSLTT unit to hand, here's what you'll need to do to get up and running.
{: .fs-6 .fw-300 }


## Install The Software

Head to [the releases page](https://github.com/OSRTT/OSLTT/releases/latest) and download the "OSLTT Installer.exe" file. When you run it Windows will likely say this is an untrusted file, you'll need to click the "more info" link/button, then "Run Anyway". I'll fix that as soon as I work out how... 

Anyway, run the installation wizard as usual. It will run the program after you finish (by default anyway). 

You'll be greeted with a message box asking if you want to let the program continue with further setup. You'll need to select yes to make the tool work. 

This installs required Arduino and SEEED libraries and the required drivers too. You'll need to click "Install" on both driver pop-ups. 

It may also ask you to do a firmware update on the board. Updating to the most recent version is almost always recommended

## Settings

There are a number of presets that pre-select the correct options to best test the various options. These include:
* Monitor - uses the DirectX test mode, button trigger and light sensor
* Mice/Keyboards - uses the click/keypresses input and mouse/keyboard test source
* Games - uses the light sensor, built in button and game test source
* Headsets - uses the audio sensor, button trigger and audio clip source
* Custom - this enables all options for you to select what works best for you

## Running a test
The best test to start with is likely the monitor testing mode. After selecting the "Monitor" preset, hit the "Start" button - or press F10 to do the same thing - then your selected display will go black as the DirectX window launches. Give it a moment to start up fully - the FPS counter in the top left should sit at ~1000FPS. Ensure your OSLTT unit is attached light-sensor-side-down to your selected display. You can then press the button on the OSLTT unit, which should make the screen start flashing white. Once it completes the default 100 clicks, the DirectX window will close and the results view window will open.