---
description: >-
  ROS implementation and specific features implemented by Cyril and Nathan for
  the ROV BlueRov2
---

# aColor-BlueRov2 ROS implementation

## Some useful acronyms

* ROV : Remotely Operated underwater Vehicles
* AUV : Autonomous Underwater Vehicles
* ROS : Robot Operating System
* aColor : Autonomous and Collaborative Offshore Robotics
* IMU : Inertial Measurement Units
* DVL : Doppler Velocity Log
* GPS : Global Positioning System
* USBL : Ultra-short baseline
* ESC : Electronic Speed Control
* DOF : Degree Of Freedom 

## BlueRov2 

The BlueRov2 is a small Remotely Operated Vehicle \(ROV\) made and sold by the company Bluerobotics. The BlueRov2 that we worked on has:

* 6 Thrusters T200
* 6 Basic Esc
* 1 Bar30 pressure sensor 
* 2 Leak sensors
* 4 Lumen Subsea Lights
* 1 Raspberry Pi 3B, used as a companion computer
* 1 camera
* 1 servo for the camera tilt
* 1 PixHawk \(Px4-v2\) : with internal 9 DOF IMU
* 2 Adafruit LSM9DS1 9DOF
* 1 Fathom ROV tether

A more detailed list of the ROV component can be found at [https://bluerobotics.com/store/rov/bluerov2/bluerov2/](https://bluerobotics.com/store/rov/bluerov2/bluerov2/)

## Connection

According to the ArduSub documentation, the BlueRov2 requires a tether to be linked to a topside computer. Image 1 shows a diagram of how it is connected to a topside controller with the ROS implementation.

QGroundControl can be used to set up various parameters and to pilot manually the robot while having the view of the camera.

ROS is used to compute command laws from sensors data. These commands are PWM values for the motors inside the BlueROV2. 

![Image 1 : Connection model](.gitbook/assets/acolorbluerov2softdiagram.png)

