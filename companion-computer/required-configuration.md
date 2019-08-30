# Required configuration

## ardware

:ccording to the ArduSub project, the companion computer must be a Raspberry Pi 3 model B \(not B+\) to ensure complete support.

## Software

The raspberry Pi need the companion computer image from BlueRobotics. You can find [here](https://www.ardusub.com/getting-started/installation.html#ardusub) how to install the latest image.

If you want to use the two additional IMUS, you can use the image _aColor-BlueRov2-raspberry-with-server-for-imu-4Gb.img_ that comes with all dependencies for the ROV and the IMUS.

## MavProxy parameters

To run QGroundControl \(QGC\) and and our scripts, you will need this parameters to set two end points for mavlink stream : 192.168.2.255:14550 \(QGC\) and 192.168.2.1:14560\(ROS bridge\)

Here is the parameters to past in the file mavproxy.param in /home/pi of companion computer

```text
--master=/dev/autopilot,115200
--load-module='GPSInput,DepthOutput'
--source-system=200
--cmd="set heartbeat 0"
--out udpin:localhost:9000
--out udpbcast:192.168.2.255:14550
--out udpbcast:192.168.2.1:14560
--mav20
--aircraft telemetry
--streamrate -1
```

{% hint style="info" %}
To access the file without open the BlueRov2 you can power and connect the ROV to the topside computer and use the web interface : [http://192.168.2.2:2770/mavproxy](http://192.168.2.2:2770/mavproxy)
{% endhint %}

## Internal Raspberry Pi system

### Processes running

At the start of the Raspberry Pi, few processes started : MAVproxy, a server for IMUs, processes for web interface.

### Access internal system

#### SSH

You can access Raspberry Pi internal system via SSH. There is no graphical desktop everything must be done by command line or by the companion Web interface.

```text
ssh pi@192.168.2.2
```

The password is _companion_.

#### Companion Web interface

Companion computer hosts a web interface with useful different pages for accessing parameters and functionalities associated with Companion computer. See [https://www.ardusub.com/operators-manual/companion-web.html](https://www.ardusub.com/operators-manual/companion-web.html)

## More information

See [https://www.ardusub.com](https://www.ardusub.com)

