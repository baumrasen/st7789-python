# Info for this fork

## Intro
I use the "Pirate Audio: Line-out for Raspberry Pi" with a Raspberry Pi Zero as an webradio. To use it with MPD, I installed the [Raspberry Pi Internet Radio](https://github.com/bobrathbone/piradio6). 

## Problem
After some time (~4 hours) the display freezed and I found a segfault in the log-files:

`Fatal Python error: Segmentation fault 
Thread 0xb4655460 <python> (most recent call first): 
 File "/usr/lib/python2.7/SocketServer.py", line 150 in _eintr_retry 
 File "/usr/lib/python2.7/SocketServer.py", line 231 in serve_forever 
 File "/usr/lib/python2.7/threading.py", line 754 in run 
 File "/usr/lib/python2.7/threading.py", line 801 in __bootstrap_inner 
 File "/usr/lib/python2.7/threading.py", line 774 in __bootstrap 
Current thread 0xb6f4c010 <python> (most recent call first): 
 File "/usr/local/lib/python2.7/dist-packages/ST7789/__init__.py", line 171 in send 
 File "/usr/local/lib/python2.7/dist-packages/ST7789/__init__.py", line 192 in data 
 File "/usr/local/lib/python2.7/dist-packages/ST7789/__init__.py", line 344 in display
 File "/usr/share/radio/st7789tft_class.py", line 77 in update 
 File "/usr/share/radio/display_class.py", line 256 in update 
 File "/usr/share/radio/display_class.py", line 241 in out 
 File "/usr/share/radio/radiod.py", line 1173 in displayCurrent 
 File "/usr/share/radio/radiod.py", line 232 in process 
 File "/usr/share/radio/radiod.py", line 142 in run 
 File "/usr/share/radio/radio_daemon.py", line 125 in begin 
 File "/usr/share/radio/radio_daemon.py", line 97 in nodaemon 
 File "/usr/share/radio/radiod.py", line 1403 in <module> 
radiod.service: Main process exited, code=killed, status=11/SEGV 
radiod.service: Failed with result 'signal'. `

## Solution
I found a similar porblem [here](https://github.com/pimoroni/st7735-python/commit/3009ef94c36373866dca9ccd4313b4d1339be075) 
and modified the code.
For me it is working now without any segfault.


# Python ST7789

[![Build Status](https://travis-ci.com/pimoroni/st7789-python.svg?branch=master)](https://travis-ci.com/pimoroni/st7789-python)
[![Coverage Status](https://coveralls.io/repos/github/pimoroni/st7789-python/badge.svg?branch=master)](https://coveralls.io/github/pimoroni/st7789-python?branch=master)
[![PyPi Package](https://img.shields.io/pypi/v/st7789.svg)](https://pypi.python.org/pypi/st7789)
[![Python Versions](https://img.shields.io/pypi/pyversions/st7789.svg)](https://pypi.python.org/pypi/st7789)


Python library to control an ST7789 TFT LCD display

Designed specifically to work with a ST7789 based 240x240 pixel TFT SPI display. (Specifically the [1.3" SPI LCD from Pimoroni](https://shop.pimoroni.com/products/1-3-spi-colour-lcd-240x240-breakout)).

![Animated GIF showing the ST7789 SPI LCD displaying Deploy/Rainbows in alternating frames](https://raw.githubusercontent.com/pimoroni/st7789-python/master/square-lcd-breakout-1.gif)

# Installation

Make sure you have the following dependencies:

````
sudo apt-get update
sudo apt-get install python-rpi.gpio python-spidev python-pip python-pil python-numpy
````

Install this library by running:

````
sudo pip install st7789
````

See example of usage in the examples folder.


# Licensing & History

This library is a modification of a modification of code originally written by Tony DiCola for Adafruit Industries, and modified to work with the ST7735 by Clement Skau.

To create this ST7789 driver, it has been hard-forked from st7735-python which was originally modified by Pimoroni to include support for their 160x80 SPI LCD breakout.

## Modifications include:

* PIL/Pillow has been removed from the underlying display driver to separate concerns- you should create your own PIL image and display it using `display(image)`
* `width`, `height`, `rotation`, `invert`, `offset_left` and `offset_top` parameters can be passed into `__init__` for alternate displays
* `Adafruit_GPIO` has been replaced with `RPi.GPIO` and `spidev` to closely align with our other software (IE: Raspberry Pi only)
* Test fixtures have been added to keep this library stable

Pimoroni invests time and resources forking and modifying this open source code, please support Pimoroni and open-source software by purchasing products from us, too!

Adafruit invests time and resources providing this open source code, please support Adafruit and open-source hardware by purchasing products from Adafruit!

Modified from 'Modified from 'Adafruit Python ILI9341' written by Tony DiCola for Adafruit Industries.' written by Clement Skau.

MIT license, all text above must be included in any redistribution
