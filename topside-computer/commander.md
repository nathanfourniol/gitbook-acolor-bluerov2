---
description: description of the file commander.py
---

# Commander

The class Commander deals with the publication of pwm to the RC\_channels topics that leads to the motion of the BlueRov2

| ROS topics subscribed | Message | Function |
| :---: | :---: | :---: |
| /Command/depth |  | pwm sent by [depth controller](controllers/depth-control.md) |
| /Command/heading |  | pwm sent by [heading controller](controllers/heading-control.md) |
| /Command/velocity |  | pwm sent by [velocity controller](controllers/velocity-control.md) |
| /Command/joy |  | pwm and buttons clicked sent by [gamepad](controllers/gamepad.md) |
| /Settings/set\_depth |  | enable to send pwm to thrusters |
| /Settings/set\_heading |  | enable to send pwm to thrusters |
| /Settings/set\_velocity |  | enable to send pwm to thrusters |

| ROS topics published | Message | Function |
| :---: | :---: | :---: |
| /BlueRov2/rc\_channel3/set\_pwm |  | Throttle |
| /BlueRov2/rc\_channel4/set\_pwm |  | Yaw |
| /BlueRov2/rc\_channel5/set\_pwm |  | Forward |
| /BlueRov2/rc\_channel6/set\_pwm |  | Lateral |
| /BlueRov2/rc\_channel8/set\_pwm |  | Camera tilt |

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

According to MAVlink, only 8 first channels can be overridden, to reach the other channels, it's needed to send MAVlink command with manual\_command\_sent 
{% endhint %}

## Modes

There are two modes in commander : the MANUAL mode where the gamepad controls the ROV or the AUTOMATIC mode where depth, heading and velocity pwm computed by the controllers drive the ROV if there are enable to be published.

## Enable controllers

To enable controllers to control the ROV, you have to send a Set\_\[depth/heading/velocity\] message with the parameter enable\_\[depth/heading/velocity\]\_ctrl to True. Otherwise, the ROV remains uncontroled by the controllers.

