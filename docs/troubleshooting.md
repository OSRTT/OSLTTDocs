---
layout: default
title: Troubleshooting
nav_order: 7
---

# Troubleshooting
{: .no_toc }


Things happen. Testing response times is 50% a science, 50% an art, so you are bound to run into issues. Here's a few tips and common issues.
{: .fs-6 .fw-300 }


## Backlight Strobing

You might get a warning that the display's backlight is strobing. You can easily verify how badly by looking at the brightness calibration "raw result". If it stays within 300 to 500 points without any changes (i.e brightness, moving the unit, e.t.c), it's perfectly fine. If the level changes more drastically, you might have issues with the data processing. If you see the "raw result" value drop by thousands of points you might have a display that is actively turning the backlight off for some portion of the frame. That is something you wouldn't be able to measure effectively.

## Data failed to process

The data may fail to process for a number of different reasons - the best thing to do is load up the raw data as a graph in the Results View window (Heatmaps & Graphs button) as that will almost always show what's going wrong.

### Capture Time Too Short

If the "capture time" setting is set too short - either because VSync is enabled which adds two or three frames of input latency, because the display has terrible input latency, or because the panel is so slow the transition is still running when the device stops capturing - the graph will look like it's cut short. The graph should have a clear, flat, steady-state start and end. If the transition is still running when the capture window ends, the processing code won't be able to pick the end point effectively. 

### Too Noisy

The data can be noisy for a number of reasons. The USB input power may be noisy, to verify this (with the sensor covered/on your desk) press the "Save USB Voltage Readout" setting in the "Debugging Tools" menu. This will save a CSV (comma separated values) file to the \Results folder. Check the data in Excel (or data viewer of your choice) - it should be as close to a flat line as possible. Some noise is expected but hundreds-of-point-swings aren't ideal. If that's the case, try a different port, powered hub or device.

If your USB power is stable, then it's more likely it's the monitor that's the issue. If the noise is small separate spikes, especially at regular intervals, that's often the display refreshing (badly). Try moving the unit, or rotating it 90°. If it's just a wide noise range over otherwise clear data, that may be because the brightness level isn't set quite right. Try increasing the brightness of the display slightly and run the test again.


# Version Rollback
If you've recently updated to a newer version of the response time tool software or firmware and want to roll back to an earlier version, you can do so from version 3.1 onwards. It's best to uninstall your current version - making sure to backup your Results folder - then download the installer for the version you'd like to step back to. 

You will then need to match the device firmware version with the software version it was designed for. You can do that by launching the software, then in the menu bar at the top clicking "Debugging Tools", then "Update Device Firmware". This will tell you the device has the newest firmware, but will ask if you want to flash the saved version anyway. Click yes, then let it install the older firmware file. Once done you should be back to the same condition prior to updating. 
