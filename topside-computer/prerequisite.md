---
description: Dependencies to run our codes
---

# Required configuration

## OS

Ubuntu 16.04

## Network settings : IP configuration

Topside computer must be at the address 192.168.2.1

## Dependencies

* Python 2.7
* PyMavlink
* PyYAML
* Opencv-Python \(only if you want to see camera with video script from bluerov\_ros\_playground\)
* Numpy
* [Inputs](https://github.com/zeth/inputs) 
* [gi,gobject](https://wiki.ubuntu.com/Novacut/GStreamer1.0)
* PyQt5
* ROS kinetic

## ROS package

Get ROS package at : [https://github.com/cyrilcotsaftis/bluerov\_ros\_playground](https://github.com/cyrilcotsaftis/bluerov_ros_playground) and clone it in src/ folder of your ros workspace

```text
git clone https://github.com/cyrilcotsaftis/bluerov_ros_playground
cd bluerov_ros_playground
git submodule update --init --recursive
```

{% hint style="info" %}
This ROS package is build on the Patrick J. Pereira bluerov\_ros\_playground accessible at [https://github.com/patrickelectric/bluerov\_ros\_playground](https://github.com/patrickelectric/bluerov_ros_playground) 
{% endhint %}

Then you will need to build the workspace.

```text
catkin build #if you use catkin build
catkin_make  #if you use catkin_make
```

{% hint style="warning" %}
catkin build and catkin\_make are not compatible tools to build ROS workspace.
{% endhint %}

