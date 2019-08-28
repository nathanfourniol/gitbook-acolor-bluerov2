---
description: description of velocity_controller.py
---

# Velocity control

{% hint style="danger" %}
Not working as controller because of difficulties to estimate velocity see [here](velocity-control.md#velocity-estimation). The controller publishes only a constant pwm from the velocity target between \[-400,400\] plus 1500 to be in \[-1100,1900\] for thrusters.
{% endhint %}

The class Velocity\_controller had the aim to implement a PD controller in order to reach the velocity desired but the aim was not reach.

## **ROS**

### Node

velocity\_controller

### Topics

| ROS topics subscribed | Message | Description |
| :---: | :---: | :--- |
| /imu/imu\_raw | sensors\_data/imu | X axis acceleration |
| /Settings/set\_velocity | bluerov\_ros\_playground/Set\_velocity | Settings for the controller |
| /Settings/set\_target | bluerov\_ros\_playground/Set\_target | velocity to reach, |

| ROS topics published | Message | Description |
| :---: | :---: | :--- |
| /Command/velocity | Uint16 | Pwm send by the controller to the commander |

## Velocity estimation

To estimate current velocity only from acceleration, it is needed to integrate acceleration values once. However, raw IMU data are noisy and even after the use of filters in the Imu data publisher, errors remain. A drift is then observed over time on the velocity estimation. This script cannot be use as a velocity controller yet.

{% hint style="warning" %}
Yet if you enable the controller in AUTOMATIC mode, it will send a constant pwm equals to pwm\_max - 50 where pwm\_max is defined in Set\_velocity message published on the topic /Settings/set\_velocity
{% endhint %}

## PD controller

The PD controller use the difference between velocity calculated and velocity desired, but also the derivative and the integrate value to compute a command in the interval \[-400,+400\]. This command is add to 1500, the pwm neutral of thrusters.

## Saturation

A saturation method is added on pwm output before the publication on the command topic in order to limit thruster power.

## Send velocity target

The velocity target is defined by the publication of a Set\_target message on the topic /Settings/set\_target. This message is shared with the depth and the heading controller to set their target.

{% hint style="danger" %}
The velocity target in a pwm between \[-400,400\] that will be added to 1500. There is no PD controller on velocity. The pwm sends is a constant pwm.
{% endhint %}

{% hint style="info" %}
Several methods exist to publish the message : the GUI, command line, script, ....
{% endhint %}

| Set\_target message : |  | Units |
| ---: | :--- | :--- |
| float64 | depth\_desired | m |
| float64 | heading\_desired | deg |
| float64 | velocity\_desired | pwm range \[-400,400\] |

## Tune PD and set saturation

PD coefficients and maximum pwm for saturation of the command can be modified in real time by the Set\_velocity message published on the topic /Settings/set\_velocity.

{% hint style="danger" %}
These values sent are not saved and the controller will get its initial value. To change permanently the values of those parameters you must change it in the code, in the \_\_init\_\_ method.
{% endhint %}

| Set\_depth message |  |
| ---: | :--- |
| bool | enable\_velocity\_ctrl |
| uint16 | pwm\_max |
| uint32 | KP |
| uint32 | KD |

{% hint style="info" %}
See [Commander](../commander.md) to know how enable\_velocity\_ctrl is used
{% endhint %}

