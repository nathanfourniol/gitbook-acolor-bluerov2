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

