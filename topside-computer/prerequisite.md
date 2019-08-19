# Required configuration

## OS

Ubuntu 16.04

## Network settings : IP configuration

Topside computer must be at the address 192.168.2.1

## Dependencies

* PyMavlink
* PyYAML
* Opencv-Python
* Numpy
* [gi,gobject](https://wiki.ubuntu.com/Novacut/GStreamer1.0)
* PyQt5
* ROS kinetic

## ROS package

Get ROS package at : [https://github.com/cyrilcotsaftis/bluerov\_ros](https://github.com/cyrilcotsaftis/bluerov_ros)

```text
git clone https://github.com/cyrilcotsaftis/bluerov_ros
cd bluerov_ros
git submodule update --init --recursive
```

{% hint style="info" %}
This ROS package is build on the Patrick J. Pereira bluerov\_ros\_playground accessible at [https://github.com/patrickelectric/bluerov\_ros\_playground](https://github.com/patrickelectric/bluerov_ros_playground) 
{% endhint %}

