> [!WARNING]
> This fork of [WiROS](https://github.com/ucsdwcsng/WiROS) is a complete rewrite done to expose certain information necessary for research not exposed in a useful way by the original library. As such, it makes many breaking API changes. This is not a drag-and-drop replacement for the original WiROS. This repository also implements only the WiROS capabilities we need, and _there are no guarantees that every WiROS feature is implemented here!_

# WiROS: WiFi sensing toolbox for robotics

WiROS is a plug-and-play WiFi sensing toolbox allowing researchers to access coarse grained WiFi signal strength (RSSI), fine grained WiFi channel state information (CSI), and other MAC-layer information (device address, packet IDs, or frequency-channel information). Additionally, WiROS open-sources state-of-art CSI calibration methods and direction-finding algorithms.

This repository consists of several ROS packages:

1. [**wiros_csi**](wiros_csi/) - ROS wrapper for the Nexmon CSI toolkit[1]
2. [**wiros_processing**](https://github.com/Jklein64/wiros_processing/) - calibration and direction-finding algorithms
3. [**rf_msgs**](https://github.com/Jklein64/rf_msgs/) - ROS messages to structure WiFi measurement information

## Overview of Features

1. Easily integrate WiFi CSI, RSSI, and other WiFi MAC-layer information into your robot sensor stack.
2. Exposes all relevant measurements as accessible ROS topics. See **rf_msgs** for more details.
3. Open-sources implementation of various state-of-art WiFi processing algorithms[2, 3, 4].

## Getting Started

To get started with WiROS, recursively clone this repo into your catkin workspace's `src/` folder

```bash
git clone --recursive https://github.com/Jklein64/wiros.git
```

Then `cd` to the workspace root and build with

```bash
catkin_make
```

Follow the [README](https://github.com/ucsdwcsng/wiros_csi_node/blob/main/README.md) in the [CSI Node](https://github.com/ucsdwcsng/wiros_csi_node) to configure your hardware.

Once configured, running the `csi_node` from **wiros_csi** will publish raw CSI data to `/csi_raw`. We recommend passing the raw data through `correction_node.py` from **wiros_processing** before extracting AoA information with `aoa_node.py`.

## Example usage of WiROS

WiROS can be easily leveraged to incorporate WiFi sensors to solve many applicable problems in robotics. We provide the following sample use-cases:

1. **Kidnapped Robot Problem**: A lost robot in an indoor envrionment can be conveniently localized using WiROS. Given a prior map of the existing Access points and additional details of their antenna geometry, the robot's location can be triangulated in a space.
2. **Correct for Robot Location Drift**: WiFi measurements can be additionally fused with Camera and odometry measurements to more accurately correct for sensor drifts and resolve ambiguities arising from perceptual aliasing in indoor environment[3].
3. **IoT device localiztion**: Often IoT devices are hard to localize visually. However, we can leverage WiFi-based bearing measurements to trinagulate their position in the envrionment. This can be useful for both IoT device management or to ensure security/privacy of users in a space.

## Citations

1. Blanco, Alejandro, et al. "Accurate ubiquitous localization with off-the-shelf ieee 802.11 ac devices." The 19th Annual International Conference on Mobile Systems, Applications, and Services (MobiSys 2021). 2021.
2. Kotaru, Manikanta, et al. "Spotfi: Decimeter level localization using wifi." Proceedings of the 2015 ACM Conference on Special Interest Group on Data Communication. 2015.
3. Arun, Aditya, et al. "ViWiD: Leveraging WiFi for Robust and Resource-Efficient SLAM." arXiv preprint arXiv:2209.08091 (2022).
4. Schmidt, Ralph. "Multiple emitter location and signal parameter estimation." IEEE transactions on antennas and propagation 34.3 (1986): 276-280.
