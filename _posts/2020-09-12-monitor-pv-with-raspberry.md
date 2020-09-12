---
layout: post
title: PV Web Interface with Raspberry Pi
desc: In this post I will explain you how to set up a Raspberry Pi in order to monitor a photovoltaic domestic system. The Raspberry communicates with a Aurora Power One inverter, but the procedure can be easily adapted to different inverters, provided they are equipped with serial communication. You find the repository on GitHub.
---

In this post I will explain you how to set up a Raspberry Pi in order to monitor a photovoltaic domestic system. 
The Raspberry communicates with a Aurora Power One inverter, but the procedure can be easily adapted to different inverters, provided they are equipped with serial communication.
You find the repository on GitHub.

## Hardware

The following hardware is required:
- Raspberry Pi (3b+ is used in this case).
- Telephone cables for serial communication.

## Software

The web-interface is written in python and Flask.
The .html and .css makes use of no modules. Interactive plots are generated with bokeh.

![image](/assets/img/pv_dashboard.png)
