# Velocity control

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
| depth | current depth | m |
| p | pressure measured | Pa |
| p0  | surface pressure | 99 000Pa |
| ρ  | water density | 1000 kg/m³ |
| g | gravitational acceleration | 9.81 kg/m² |

## PID controller

The PID controller use the difference between depth calculated and depth desired, but also the derivative and the integrate value to compute a command in the interval \[-400,+400\]. This command is add to 1500, the pwm neutral of thrusters.

## Saturation

A saturation method is added on pwm output before the publication on the command topic in case of a will to limit thruster power.  

## Send depth target

The depth target is defined by the publication of a Set\_target message on the topic /Settings/set\_target. This message is shared with the heading and the velocity controller to set their target

{% hint style="info" %}
Several methods exist to publish the message : the GUI, command line, script, ....
{% endhint %}

| Set\_target message :  |  | Units |
| ---: | :--- | :--- |
| float64 | depth\_desired | m |
| float64 | heading\_desired | deg |
| float64 | velocity\_desired | m/s |

{% hint style="warning" %}
In this script, the axis Z for the depth goes up. To reach 1m depth the input must be -1
{% endhint %}

## Tune PID and set saturation

PID coefficients and maximum pwm for saturation of the command can be modified in real time by the Set\_depth message published on the topic /Settings/set\_depth. 

{% hint style="danger" %}
 These values send are not saved and the controller will get its initial value. To change permanently the values of those parameters you must change it in the code, in the \_\_init\_\_ method.
{% endhint %}

| Set\_depth message |  |
| ---: | :--- |
| bool | enable\_depth\_ctrl |
| uint16 | pwm\_max |
| uint32 | KI |
| uint32 | KP |
| uint32 | KD |

{% hint style="info" %}
See [Commander](../commander.md) to know how enable\_depth\_ctrl is used
{% endhint %}

