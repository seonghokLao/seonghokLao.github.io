---
title: Ping Pong Localization
layout: template
filename: pingpong-localization.md
--- 
# Ping Pong Localization
This repository aims to get a state estimation of a ping pong paddle based on a [YOST Labs 3-Space Mini Wireless IMU](https://yostlabs.com/product/wireless-mini/) and a ZED 2 camera's body tracking feature.

<p align="center">
    <img src="ping_pong_skeleton.gif" alt="Ping Pong Skeleton" width="400"/>
</p>

## Files
* `data/`: Stores data for body tracking and IMU points
* `threespace/updated_ThreeSpaceAPI/`: Houses the updated 3-Space API for the wireless IMU
* `threespace/IMU_Class.py`: Wrapper class for the wireless IMU
* `threespace/imu_ros.py`: Runs the wireless IMU ROS node
* `threespace/USB_Class.py`: Serial class to connect to the wireless IMU
* `zed_sdk/body_tracking/body_tracking_ros.py`: Runs the ZED body tracking ROS node
* `zed_sdk/image_capture/test_camera_pose.py`: Outputs figures of the skeleton and IMU axes from the output data
* `time-sync.py`: Subscribes to the IMU and body tracking messages to sync and save them to numpy files

## Setup
In order to setup this repository the following packages and libraries need to be installed on Ubuntu 20.04:
* OpenCV
* [ZED SDK](https://www.stereolabs.com/developers/release)
* ROS Noetic
* numpy
* matplotlib

In order to setup the wireless IMU, follow these steps:
1. On Windows, download the [3-Space Sensor Suite](https://yostlabs.com/yost-labs-3-space-sensor-software-suite/)
2. Connect the [3-Space Wireless Dongle](https://yostlabs.com/product/3-space-wireless-dongle/) to your computer and click connect in the suite after selecting the correct COM port
3. Select dongle info from the dongle menu and in logical ID 0 input the serial number on the back of the wireless IMU (Note: As of testing it in May 2024, the dongle only supports one logical ID at a time)
4. Press **Commit Settings**

## Installation
1. Run `threespace/imu_ros.py` to start the wireless IMU and publish on `/imu/data`
2. Run `zed_sdk/body_tracking/body_tracking_ros.py` to start the ZED body tracking and publish on `keypoints`
3. Run `time-sync.py` to start syncing the IMU and body tracking data
4. When satisfied with a run, quit out of `time-sync.py` to save the points
5. Run `zed_sdk/image_capture/test_camera_pose.py` to output figures of the skeleton and IMU axes
