# Pymavlink

There is a lot of examples for BlueRov2 [https://www.ardusub.com/developers/pymavlink.html](https://www.ardusub.com/developers/pymavlink.html) 

There is two end points for mavlink stream :

|  |  |
| :--- | :--- |
| 'udpin:192.168.2.1:14550' |  used by QGroundControl \(QGC\) but if QGC is not launch you can use this end point |
| 'udpin:192.168.2.1:14560' | used by bluerov2\_node to do the bridge between ROS and MAVlink  |

## Change MAVlink protocol from version1 to version 2

Currently the MAVlink protocol version 1 is used.

If you want to use the  MAVlink protocol version 2 you will need to change the STREAM\_PARAMETER with QGroundControl \(or mavlink command but it is more difficult\) for PixHawk. Then you will need to setup pymavlink environment to work with Mavlink 2. Here it is a quotation from [https://mavlink.io/en/mavgen\_python/](https://mavlink.io/en/mavgen_python/) to deal with protocol.  

"By default **mavutil** sets up the link to use the MAVLink 1 `ardupilotmega` dialect for sending/receiving. You can change this by setting environment variables:

* `MAVLINK_DIALECT`: Set to string name for the dialect file \(without XML extension\). For Ardusub it is _ardupilotmega_
* `MAVLINK20`: Set to 1 \(if unset then default to MAVLink 1\)
* `MDEF`: Location of message definition libraries "

