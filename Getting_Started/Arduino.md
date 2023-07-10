---
layout: default
title: Arduino
parent: Getting Started
---

# Arduino

To use the Adafruit VL53L4CD and C12880MA with the Arduino Nano Every you must first install [Arduino](https://www.arduino.cc/en/software). You'll be able to find instructions to install Arduino for your operating system on this website. 


## Arduino Nano Every

Once you download Arduino you'll need to install support for the Arduino Nano Every. The Nano Every uses the megaAVR core and you'll need to instal that first.

First open the Arduino IDE then go to Tools->Board->Board Manager. Once you open that window, type `"megaavr"` and Download `"Arduino AVR Boards by Arduino"`. To select the board go to Tools->Board->Arduino megaAVR Boards and select Arduino Nano Every. 

### Hello World!

In your Arduino IDE select, File->Examples->01.Basics and click on Blink. To upload code to the Nano Every click on the upload button (Arrow pointing to the right). Congrats! You should see the the LED turn on and off every second.

### C12880MA
For the C12880MA we use the Arduino example provided by GroupGets. The link can be found [here](https://github.com/groupgets/c12880ma).
```bash
git clone https://github.com/groupgets/c12880ma.git
cd c12880ma/arduino_c12880ma_example 
arduino arduino_c12880ma_example.ino 
```
Once you open the Arduino file you'll need to upload the file into the Arduino Nano Every. 


### Adafruit VL53L4CD	
In your Arduino IDE open Sketch->Include Library->Manage Libraries and type `"VL53L4CD"`. Now select `"STM32duino VL53L4CD by SRA"`.
Now select File->Examples->Arduino VL53L4CD->VL53L4CD_Sat_HelloWorld. Select the port for your second Arduino Nano Every upload the code. 