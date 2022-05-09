# Power10 App

## Overview

Power10 is a sport performance sensor that measures 3D accelerations in real-time to help athletes improve their
performance.  It is mainly designed for rowing, canoeing and kayaking but can be used in any application requiring real-time acceleration data logging.  It works with an app for phone or tablet that lets the user log, view and share acceleration data from their training session.

This repository contains the code for the app.

The app communicates with the Power10 sensor using Bluetooth Low Energy (BLE).  When enabled (by hitting the record button on the app), the sensor will send BLE notify messages every 100ms to the app.  Each message contains 10 acceleration samples taken at a 10ms period.  Each sample has three 16b signed integers representing X, Y and Z axis acceleration where:

- X is in line with the axis of the boat 
- Y is perpendicular to the axis of the boat
- Z is vertical

The acceleration full scale is 2g.  So the 16b range of -32768:+37767 represents accelerations on the range of -2g:+2g.
The X and Y readings will be close to 0 with no acceleration while the Z will show close to 16384 when not moving representing 1g i.e. the force of gravity.  Variations about these ideal values are possible if the sensor is not mounted perfectly level when at rest.

In addition to the acceleration data, each message contains a 1byte sequence number that can be used to detect missing messages.

The sensor samples acceleration every 2.5ms and averages 4 samples for each of the 10ms samples.

## Tools Used
- Flutter

## Plug-ins Used
- flutter_blue_plus
