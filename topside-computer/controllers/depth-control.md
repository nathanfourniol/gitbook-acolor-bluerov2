---
description: description of the file depth_controller.py
---

# Depth control

The class Depth\_Control implements a PID controller in order to reach the depth desired.

## ROS topics

| ROS topics subscribed | Message | Function |
| :---: | :---: | :---: |
| /BlueRov2/bar30 | bluerov\_ros\_playground/Bar30 | Absolute pressure in hPa |
| /Settings/set\_depth | bluerov\_ros\_playground/Set\_depth | Settings for the controller |
| /Settings/set\_target | bluerov\_ros\_playground/Set\_target | Depth to reach, vertical axis goes up  |

{% hint style="warning" %}
In this script, the axis Z for the depth goes up. To reach 1m depth the input must be -1
{% endhint %}

| ROS topics published | Message | Function |
| :--- | :--- | :--- |
| /Command/depth | Uint16 | Pwm send by the controller to the commander |

## Depth estimation

To estimate current depth the controller get the absolute pressure from the Bar30 sensor and compute it with hydrostatic equation.

$$
depth = -(p - p0) / (ρ * g)
$$

| Designation | Meaning | Value |
| :---: | :---: | :---: |
| p | pressure measured | Pa |
| p0  | surface pressure | 99 000Pa |
| ρ  | water density | 1000 kg/m³ |
| g | gravitational acceleration | 9.81 kg/m² |

## PID controller

The PID controller use the difference between depth calculated and depth desired, but also the derivative and the integrate value to compute a command in the interval \[-400,+400\]. This command is add to 1500, the pwm neutral of thrusters.

## Saturation

A saturation method is added before the publication on the command topic in case of a will to limit thruster power.

## Send depth target

The depth target is defined by the publication of a Set\_target message on the topic /Settings/set\_target. There are several methods to publish on this topic : the GUI, command line, script, ...

Set\_target message : 

| Type | Field name |
| :--- | :--- |
| float64      | depth\_desired |
| float64 | heading\_desired |
| float64 | velocity\_desired |

```text
rostopic publish -? message
```

## Tune PID and set saturation

To change PID coefficient you can use the GUI

