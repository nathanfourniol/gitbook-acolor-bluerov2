---
description: description of velocity_controller.py
---

# Velocity control

{% hint style="danger" %}
Not working as controller yet because of difficulties to estimate velocity see [here](velocity-control.md#velocity-estimation)
{% endhint %}

The class Velocity\_controller implements a PD controller in order to follow the heading desired.

## ROS topics

| ROS topics subscribed | Message | Function |
| :---: | :---: | :---: |
| /imu/imu\_raw | sensors\_data/imu | X axis acceleration |
| /Settings/set\_velocity | bluerov\_ros\_playground/Set\_velocity | Settings for the controller |
| /Settings/set\_target | bluerov\_ros\_playground/Set\_target | velocity to reach, |

| ROS topics published | Message | Function |
| :---: | :---: | :---: |
| /Command/depth | Uint16 | Pwm send by the controller to the commander |

## Velocity estimation

To estimate current velocity only from acceleration, it is needed to integrate acceleration values once. Even with the filters in the Imu data publisher, a drift cannot be removed leading to a false velocity estimation. Indeed this script cannot be use yet as a velocity controller.

{% hint style="warning" %}
Yet if you enable the controller in AUTOMATIC mode, it will send a constant pwm equals to pwm\_max - 50 where pwm\_max is defined in Set\_velocity message published on the topic /Settings/set\_velocity
{% endhint %}

## PID controller

The PID controller use the difference between depth calculated and depth desired, but also the derivative and the integrate value to compute a command in the interval \[-400,+400\]. This command is add to 1500, the pwm neutral of thrusters.

## Saturation

A saturation method is added on pwm output before the publication on the command topic in case of a will to limit thruster power.

## Send velocity target

The velocity target is defined by the publication of a Set\_target message on the topic /Settings/set\_target. This message is shared with the depth and the heading controller to set their target.

{% hint style="danger" %}
This not work for velocity target see [here](velocity-control.md#velocity-estimation)
{% endhint %}

{% hint style="info" %}
Several methods exist to publish the message : the GUI, command line, script, ....
{% endhint %}

| Set\_target message : |  | Units |
| ---: | :--- | :--- |
| float64 | depth\_desired | m |
| float64 | heading\_desired | deg |
| float64 | velocity\_desired | m/s |

## Tune PID and set saturation

PID coefficients and maximum pwm for saturation of the command can be modified in real time by the Set\_velocity message published on the topic /Settings/set\_velocity.

{% hint style="danger" %}
These values send are not saved and the controller will get its initial value. To change permanently the values of those parameters you must change it in the code, in the \_\_init\_\_ method.
{% endhint %}

| Set\_depth message |  |
| ---: | :--- |
| bool | enable\_velocity\_ctrl |
| uint16 | pwm\_max |
| uint32 | KI |
| uint32 | KP |
| uint32 | KD |

{% hint style="info" %}
See [Commander](../commander.md) to know how enable\_velocity\_ctrl is used
{% endhint %}

