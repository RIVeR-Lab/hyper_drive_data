---
title: Data Set
layout: default
---
# Data Set

## Raw Data

The raw data from each of the collections onboard the robot was collected as a ROS bagfile. These files are very large (10+ GB) and contain time synchronized messages from the cameras, onboard fiber optic inertial measurement unit (IMU), and point spectrometers. Due to the massive amount of data, and the enormous human effort required to segment these 12,874 images, we have left the majority of unlabeled, but available to the research community.

## Bag File List
<div class="code-example" markdown="1">

| Bag       | Description          |\# HSI Images|
|:-------------|:------------------|:------------------|
| [olin_collection_05_15_23_parcel_b.bag](https://robot.neu.edu/uploads/hyper_drive/olin_collection_05_15_23_parcel_b.bag)|Off-road collection, daytime|2068 |
| [olin_collection_05_15_23_parcel_b_v2.bag](https://robot.neu.edu/uploads/hyper_drive/olin_collection_05_15_23_parcel_b_v2.bag)|Off-road collection, daytime | 923   |
| [olin_collection_05_15_23_parcel_b_v3.bag](https://robot.neu.edu/uploads/hyper_drive/olin_collection_05_15_23_parcel_b_v3.bag)|Off-road collection, daytime | 1117   |
| [olin_collection_05_15_23_parcel_b_v4.bag](https://robot.neu.edu/uploads/hyper_drive/olin_collection_05_15_23_parcel_b_v4.bag)|Off-road collection, daytime| 1294   |
| [olin_collection_05_16_23_campus.bag](https://robot.neu.edu/uploads/hyper_drive/olin_collection_05_16_23_campus.bag)|On-road collection, mid-morning | 3590   |
| [olin_collection_05_16_23_parcel_b.bag](https://robot.neu.edu/uploads/hyper_drive/olin_collection_05_16_23_parcel_b.bag)|Off-road collection, dawn|2556 |
| [olin_collection_05_16_23_parcel_b_v2.bag](https://robot.neu.edu/uploads/hyper_drive/olin_collection_05_16_23_parcel_b_v2.bag)|Off-road collection, dawn| 1326   |

</div>

After downloading a bag file, start a `roscore` instance and begin the playback of messages with `rosbag plag <<BAGFILENAME>>`

{: .note }
These data cubes exist currently as digital count measurements. They will be converted to reflectance in the near future via an in-development method that leverages the included spectrometer measurement.

## Labeled data

504 images evenly distributed from each of the above bag files has been extracted and labeled.

The file `label_map.json` contains the mapping from semantic label to numeric value of the mask area. Pixels with label 0 are unlabeled.

The directory structure for the labeled data follows a structured format:

```
│
├── INSTANCE_LABELS/
│   ├── xxx.json # Image labels according to the ATLAS ontology
├── RGB_RAW/
│   ├── xxx.jpg # Raw RGB image of scene
├── SEGMENTATIONS_RAW/
│   ├── xxx.png # Semantic segmentation masks for each image, where each pixel is the class index
├── SOLAR_SPECTRA/
│   ├── xxx.npy # Spectra of observed solar illumination in numpy format
├── SWIR_RAW/
│   ├── xxx.npy # SWIR hyperspectral datacube in numpy format
└── VNIR_RAW/
    └───xxx.npy # VNIR hyperspectral datacube in numpy format
```
Each file is named with a structured format across each of the data folders.

```
bagfile_name_index.file_extension
```
Essentially, each data item is named in such as way that it can be traced back to the bag file that it came from, and the number of the sample from within that bag file. Correlating that name across the folders allows the retrieval of the full data record.

### Generating Registered Data
For the purposes of data compression, the data is stored in an unregistered format. Running the following files locally will create a registered hyperspectral datacube for each of the labeled instances.

{: .highlight}
The registration process generates datacubes that are ~80 MB each. Altogether, the full labeled dataset is ~40 GB. Make sure you have enough free space locally before executing the script!

The Jupyter Notebook [`Register_HSI.ipynb`](https://github.com/RIVeR-Lab/hyper_drive_data/blob/main/Register_HSI.ipynb) contains the functions needed to process the two hyperspectral datacubes into a single datacube. This file also appropriately crops the high-res RGB image and segmentation labels.

### Regenerating System Homographies

Registering the hyperspectral cameras is a challenging process, as their resolution is an order of magnitude less than the RGB camera. The folder `calibration` contains images from all three cameras with a precision checkerboard present. We used [keypointgui](https://github.com/Kitware/keypointgui) to manually find corresponding features. The two output homographies are saved as `.txt` files in the `calibration` folder.
