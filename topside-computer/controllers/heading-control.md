---
description: description of the file heading_controller.py
---

# Heading control

The class Heading\_controller implements a PD controller in order to follow the heading desired.

## ROS topics

| ROS topics subscribed | Message | Description |
| :---: | :---: | :--- |
| /BlueRov2/imu/attitude | bluerov\_ros\_playground/Attitude | Yaw in \[-pi,pi\]rad |
| /Settings/set\_heading | bluerov\_ros\_playground/Set\_heading | Settings for the controller |
| /Settings/set\_target | bluerov\_ros\_playground/Set\_target | Yaw to follow |

{% hint style="info" %}
The heading targeted must be in \[0, 360\]deg range where 0 is North, 180 is South
{% endhint %}

| ROS topics published | Message | Description |
| :---: | :---: | :--- |
| /Command/heading | Uint16 | Pwm send by the controller to the commander |

## Heading estimation

## PID controller

The PID controller use the difference between current yaw and the yaw desired, but also the derivative value to compute a command in the interval \[-400,+400\]. This command is add to 1500, the pwm neutral of thrusters.

{% hint style="warning" %}
To calculate the command the current yaw and the yaw desired are in \[-pi,pi\]rad range
{% endhint %}

## Sawtooth

To deal with the 2 PI modulo for angles, difference between yaw desired and current yaw goes through this function sawtooth.

## Saturation

A saturation method is added on pwm output before the publication on the command topic in case of a will to limit thruster power.

## Send heading target

The heading target is defined by the publication of a Set\_target message on the topic /Settings/set\_target. This message is shared with the depth and the velocity controller to set their target

{% hint style="info" %}
Several methods exist to publish the message : the GUI, command line, script, ....
{% endhint %}

| Set\_target message : |  | Units |
| ---: | :--- | :--- |
| float64 | depth\_desired | m |
| float64 | heading\_desired | deg |
| float64 | velocity\_desired | m/s |

{% hint style="info" %}
The heading targeted must be in \[0, 360\]deg range where 0 is North, 180 is South
{% endhint %}

## Tune PID and set saturation

PID coefficients and maximum pwm for saturation of the command can be modified in real time by the Set\_heading message published on the topic /Settings/set\_heading.

{% hint style="danger" %}
These values send are not saved and the controller will get its initial value. To change permanently the values of those parameters you must change it in the code, in the \_\_init\_\_ method.
{% endhint %}

| Set\_heading message |  |
| ---: | :--- |
| bool | enable\_heading\_ctrl |
| uint16 | pwm\_max |
| uint32 | KP |
| uint32 | KD |

{% hint style="info" %}
See [Commander](../commander.md) to know how enable\_heading\_ctrl is used
{% endhint %}

