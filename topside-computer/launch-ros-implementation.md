# Launch ROS implementation

Once the tether and the USB cable is connected to the topside computer with the right IP address you will need to execute the files that do the bridge between MAVlink message from PixHawk and ROS message on the surface computer.

## Launch the link ROS-MAVlink

```text
roslaunch bluerov_ros_playground bluerov2_node.launch
```

The ROS-MAVlink bridge use the 'udpin:192.168.2.1:14560' endpoind of mavlink stream. 192.168.2.1 is the IP address of the topside computer, and 14560 the port used. For MAVlink stream, topside computer works as server while the companion computer runing mavproxy works as a client.

{% hint style="info" %}
QGroundControl \(GQC\)use the 192.168.2.1:14550 endpoint. So you can run QGC and ROS bridge at the same time
{% endhint %}

## Launch IMU client 

To connect topside computer to a server running on companion commputer

```text
cd src/imu_i2c
python Imu_bridge.py
```

## Launch controllers and GUI

```text
roslaunch bluerov_ros_playground control.launch   
```

