---
description: description of the file gamepad.py
---

# Gamepad

The class Gamepad handle event from the Logitech Gamepad F310 connected by USB to topside computer. Build to test ROS implementation before we can connect ROS in parallel of QGroundControl \(QGC\). Because of the compatibility, the only use of gamepad is to switch between MANUAL and AUTOMATIC mode with the X button. 

{% hint style="info" %}
If you launch QGC at the same time of ROS : Disable gamepad from QGC or not launch the gamepad file.
{% endhint %}

## Library

The class gamepad use the library input from https://github.com/zeth/inputs to handle gamepad joystick and buttons.

This library comes with the github ROS repository but you will need to build it by 

```text
cd PATH2package/src/controllers/inputs
python setup.py install
```

Otherwise you can install it with pip:

```text
pip install inputs
```

## How it's working

The inputs library provides API to handle the events from gamepad. Based on the event's name, a dictionary provide a link between the name of the event and the method to call. 

### Assignation table

| Gamepad event name | Method called | Designation | Value | ArduSub/MAVlink id |
| :--- | :--- | :--- | :--- | :--- |
| ABS\_Y | \_throttle | LEFT stick vertical | \[0-128-255\] | clicked Joy : 7 |
| ABS\_X | \_lateral | LEFT stick horizontal | \[0-128-255\] | clicked Joy : 8 |
| ABS\_RZ | \_forward | RIGHT stick vertical | \[0-128-255\] | / |
| ABS\_Z | \_yaw | RIGHT stick horizontal | \[0-128-255\] | / |
| ABS\_HAT0Y | \_NDEF | LEFT cross vertical | -1 up; 0 neutral; +1 down | up : 11 ; down : 12 |
| ABS\_HAT0X | \_set\_gain\_light | LEFT cross horizontal | -1 up; 0 neutral; +1 down | left : 13 ; right : 14 |
| BTN\_TRIGGER | \_override\_controller | X | 0 ; 1  | 2 |
| BTN\_TOP1 | \_NDEF | Y | 0 ; 1 | 3 |
| BTN\_THUMB | \_NDEF | A | 0 ; 1 | 1 |
| BTN\_THUMB2 | \_NDEF | B | 0 ; 1 | 0 |
| BTN\_BASE | \_NDEF | LT | 0 ; 1 | / |
| BTN\_BASE2 | \_NDEF | RT | 0 ; 1 | / |
| BTN\_TOP2 | \_cam\_down | LB | 0 ; 1 | 9 |
| BTN\_PINKIE | \_cam\_up | RB | 0 ; 1 | 10 |
| BTN\_BASE3 | \_disarm | BACK | 0 ; 1 | 4 |
| BTN\_BASE4 | \_arm | START | 0 ; 1 | 6 |

## ROS topics

| ROS topics subscribed | Message | Function |
| :--- | :--- | :--- |
| /BlueRov2/arm | Bool |  The arm status |

| ROS topics published | Message | Description |
| :--- | :--- | :--- |
| /Command/joy | sensor\_msgs/Joy | axes : \[THROTTLE, YAW, FORWARD, LATERAL\] |
|  |  | buttons : \[ARM, OVERRIDE\_CONTROLLER, PWM\_CAM, LIGHT\_DEC, LIGHT\_INC, GAIN\_LIGHT\] |

| Parameters | Type | Description |
| :--- | :--- | :--- |
| THROTTLE | Float32 | pwm : Uint16  \[1100-1900\]range |
| YAW | Float32 | pwm : Uint16  \[1100-1900\]range |
| FORWARD | Float32 | pwm : Uint16  \[1100-1900\]range |
| LATERAL | Float32 | pwm : Uint16  \[1100-1900\]range |
| ARM | Int32 | 0 : disarm ; 1 : arm |
| OVERRIDE\_CONTROLLER | Int32 | 0 : AUTOMATIC mode, 1 : MANUAL mode |
| PWM\_CAM | Int32 | pwm for camera tilt |
| LIGHT\_DEC | Int32 | 1 if you want to decrease brightness, else 0 |
| LIGHT\_INC | Int32 | 1 if you want to increase brightness, else 0 |
| GAIN\_LIGHT | Int32 | result of gain light |

{% hint style="info" %}
The LIGHT\_DEC, LIGHT\_INC, GAIN\_LIGHT parameters are not used
{% endhint %}

