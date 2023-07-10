---
layout: default
title: Serial
parent: Getting Started
---

# Serial Without ROS

To gather data from serial without ROS you will need the following libraries:

```bash
python3 -m pip install pyserial numpy pandas matplotlib
```
or
```bash
conda install pyserial numpy pandas matplotlib
```

### Using the Spectrometers
{: .note }
You might have to change the port paths to get the spectrometers working 
```bash
cd slurp_grasping/code/data_collect
```
For the OEM Sensing Board
```bash
python3 spectrapod_new.py
```
For the C12880MA
```bash
python3 hamamatsu_new.py
```
For both
```bash
python3 data_collect.py
```
