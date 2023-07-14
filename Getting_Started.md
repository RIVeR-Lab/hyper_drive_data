---
layout: default
title: Getting Started
has_children: false
---
# Getting Started

## System Prerequisites
All code was developed and tested on Ubuntu 18-20. The raw data processing portions of this project will likely _not_ work with Windows or Mac.

## Installation

This project is built upon the Robot Operating System (ROS). If you intend to work with the raw data products, please install ROS using the [official instructions](http://wiki.ros.org/ROS/Installation)

The associated repositories [Hyper Driver](https://github.com/RIVeR-Lab/hyper_drive_public) and an [Spectrometer Drivers](https://github.com/RIVeR-Lab/spectrometer_drivers) contain the message structures needed to parse the bag file. Please clone each of these repositories into a new `catkin_ws` and `catkin build` all the project dependencies. The repositories will contain additional information on system configurations needed install dependencies.

You will also need several core library to process the raw ROS data. The file [requirements.txt](./requirements.txt) should be installed with `pip -r install requirements.txt`