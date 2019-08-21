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

[https://upcommons.upc.edu/bitstream/handle/2117/103849/MScLeslieB.pdf?sequence=1&isAllowed=y](https://upcommons.upc.edu/bitstream/handle/2117/103849/MScLeslieB.pdf?sequence=1&isAllowed=y)

Data from relatively cheap IMU sensors are very noisy. The predominant error and noise sources are: 

* constant bias error: average output of the device over a specified time, there are 2 parts one deterministic part called bias offset and a random part. The bias offset can be determined by calibration. The random part is a stochastic process and refers to the rate at which the error in an inertial sensor accumulates with time.
* bias instability: random variation in the bias computed over a finite sample of time
* angle random walk \(gyros\): white noise
* velocity random walk \(accelerometer\): white noise

To improve the quality of raw data we implemented an exponential filter \(low-pass filter to cut white noise\) and we did the calibration of the IMUs to remove the bias offset. However we could not get rid of the random bias, which cause a drift after integration.

A solution to solve the issue would be to fuse IMU acceleration data with an other measurement of velocity from an other sensor \(DVL, GPS...\) in a Kalman filter. The IMU give a good short time estimation that needs to be corrected after a while with low frequency sensors, as GPS.







