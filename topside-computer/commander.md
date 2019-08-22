---
description: description of the file commander.py
---

# Commander

The class Commander deals with the publication of pwm to the RC\_channels topics that leads to the motion of the BlueRov2

## **ROS** 

### Node

Commander

### Topics

| ROS topics subscribed | Message | Function |
| :---: | :---: | :---: |
| /Command/depth | UInt16 | pwm sent by [depth controller](controllers/depth-control.md) |
| /Command/heading | UInt16 | pwm sent by [heading controller](controllers/heading-control.md) |
| /Command/velocity | UInt16 | pwm sent by [velocity controller](controllers/velocity-control.md) |
| /Command/joy | sensor\_msgs/Joy | pwm and buttons clicked sent by [gamepad](controllers/gamepad.md) |
| /Settings/set\_depth | bluerov\_ros\_playground/Set\_depth | enable to send pwm to thrusters |
| /Settings/set\_heading | bluerov\_ros\_playground/Set\_heading | enable to send pwm to thrusters |
| /Settings/set\_velocity | bluerov\_ros\_playground/Set\_velocity | enable to send pwm to thrusters |

| ROS topics published | Message | Function |
| :---: | :---: | :---: |
| /BlueRov2/rc\_channel3/set\_pwm | UInt16 | Throttle |
| /BlueRov2/rc\_channel4/set\_pwm | UInt16 | Yaw |
| /BlueRov2/rc\_channel5/set\_pwm | UInt16 | Forward |
| /BlueRov2/rc\_channel6/set\_pwm | UInt16 | Lateral |
| /BlueRov2/rc\_channel8/set\_pwm | UInt16 | Camera tilt |

## RC Input

| Channel | Meaning |
| ---: | :--- |
| 1 | Pitch |
| 2 | Roll |
| 3 | Throttle |
| 4 | Yaw |
| 5 | Forward |
| 6 |  Lateral |
| 7 | Camera pan |
| 8 | Camera tilt |
| 9 | Light 1 level |
| 10 | Light 2 level |
| 11 | Video switch |

{% hint style="info" %}
From [https://www.ardusub.com/operators-manual/rc-input-and-output.html](https://www.ardusub.com/operators-manual/rc-input-and-output.html).

According to MAVlink and ArduSub, only the eight first channels can be overridden. To reach the other channels, the only way is to send MAVlink command with manual\_command\_sent 
{% endhint %}

## Modes

There are two modes in commander : the MANUAL mode where the gamepad controls the ROV or the AUTOMATIC mode where depth, heading and velocity pwm computed by the controllers drive the ROV if there are enable to be published.

## Enable controllers

First you need to enable AUTOMATIC mode.

Then to enable controllers to control the ROV, you have to send a Set\_\[depth/heading/velocity\] message with the parameter enable\_\[depth/heading/velocity\]\_ctrl to True. Otherwise, the ROV remains uncontrolled by \[depth/heading/velocity\] controllers.

