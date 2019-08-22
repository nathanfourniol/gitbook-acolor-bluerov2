# Pymavlink

There is a lot of examples for BlueRov2 [https://www.ardusub.com/developers/pymavlink.html](https://www.ardusub.com/developers/pymavlink.html) 

There is two end points for mavlink stream. :

|  |  |
| :--- | :--- |
| 'udpin:192.168.2.1:14550' |  used by QGroundControl \(QGC\) but if QGC is not launch you can use this end point |
| 'udpin:192.168.2.1:14560' | used by bluerov2\_node to do the bridge between ROS and MAVlink  |

## Change MAVlink protocol from version1 to version 2

Currently the MAVlink protocol version 1 is used.

If you want to use the  MAVlink protocol version 2 you will need to change the STREAM\_PARAMETER with QGroundControl or with PyMavlink. You will need also to change PyMavlink in 

