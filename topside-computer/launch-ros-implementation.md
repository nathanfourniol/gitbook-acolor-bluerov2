# Launch ROS implementation

Once the tether and the USB cable is connected to the topside computer with the right IP address you will need to execute the files that do the bridge between MAVlink message from PixHawk and ROS message on the surface computer.

## Launch the link ROS-MAVlink

```text
roslaunch bluerov_ros_playground bluerov2_node.launch
```

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

