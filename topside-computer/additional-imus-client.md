---
description: >-
  There are two additional IMUs inside the BlueRov2 to try to get a good
  estimation of the velocity
---

# Additional IMUs client

## About IMUs

IMU stands for Inertial measurement unit, they are pretty common sensors for robotics application and of course used on the BlueROV2.

The BlueROV2 has 2 kinds of IMU:

* 1 PIXhawk IMU for heading estimation
* 2 adafruit imu \(put full name\) for velocity estimation

The IMUs used have 9 DOF: 3 angular velocity, 3 linear acceleration, 3 magnetometer.

With those data it is possible to compute an orientation quaternion,  later used to calculate euler angles.

## Why 2 IMUs ?

We used 2 IMU in order to take the mean value, and therefore gain in accuracy.

\(ajouter lien research on imus + graphe influence nombre et résultat\) 

## Raw IMU data computation

Data from relatively cheap IMU sensors are very noisy. The predominant error and noise sources are: 

* constant bias error: 
* bias instability
* angle random walk \(gyros\)
* velocity random walk \(accelerometer\)









 We can decomposate the raw value like bellow:

$$
a = b
$$







