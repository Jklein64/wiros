> [!WARNING]
> This fork of [WiROS](https://github.com/ucsdwcsng/WiROS) is a complete rewrite done to expose certain information necessary for research that wasn't exposed in a useful way by the original library. As such, it makes many breaking API changes. This is not a drag-and-drop replacement for the original WiROS. This repository also implements only the WiROS capabilities we need, and _there are no guarantees that every WiROS feature is implemented here!_

# WiROS: WiFi sensing toolbox for robotics

WiROS is a plug-and-play WiFi sensing toolbox allowing researchers to access coarse grained WiFi signal strength (RSSI), fine grained WiFi channel state information (CSI), and other MAC-layer information (device address, packet IDs, or frequency-channel information). Additionally, WiROS open-sources CSI direction-finding algorithms.

This repository consists of several ROS packages:

1. [**wiros_csi**](https://github.com/Jklein64/wiros_csi/) - ROS wrapper for the [Nexmon CSI toolkit](https://github.com/seemoo-lab/nexmon_csi)
2. [**wiros_processing**](https://github.com/Jklein64/wiros_processing/) - calibration and direction-finding algorithms
3. [**rf_msgs**](https://github.com/Jklein64/rf_msgs/) - ROS messages to structure WiFi measurement information

## Overview of Features

1. Easily integrate WiFi CSI, RSSI, and other WiFi MAC-layer information into your robot sensor stack.
2. Exposes all relevant measurements as accessible ROS topics. See **rf_msgs** for more details.
3. Open-sources implementation of various WiFi processing algorithms.

## Getting Started

To get started with WiROS, recursively clone this repo into your catkin workspace's `src/` folder

```bash
git clone --recursive https://github.com/Jklein64/wiros.git
```

Then `cd` to the workspace root and build with

```bash
catkin_make
```

Follow the [CSI Node README](https://github.com/Jklein64/wiros_csi/) to configure your hardware.

Once configured, running the `csi_node` from **wiros_csi** will publish raw CSI data to `/csi_raw`. We recommend passing the raw data through `correction_node` from **wiros_processing** before extracting AoA information with `aoa_node`. The **wiros_processing** package has an [example launchfile](https://github.com/Jklein64/wiros_processing/blob/main/launch/example.launch) showing how to do this.

## Citation

Below is the BibTex citation for the original WiROS library.

```bibtex
@inproceedings{10.1145/3583120.3589817,
author = {Arun, Aditya and Hunter, William and Bharadia, Dinesh},
title = {Demo Abstract: Accessible WiFi sensing leveraging Robot Operating System},
year = {2023},
isbn = {9798400701184},
publisher = {Association for Computing Machinery},
address = {New York, NY, USA},
url = {https://doi.org/10.1145/3583120.3589817},
doi = {10.1145/3583120.3589817},
booktitle = {Proceedings of the 22nd International Conference on Information Processing in Sensor Networks},
pages = {356–357},
numpages = {2},
location = {San Antonio, TX, USA},
series = {IPSN '23}
}
```