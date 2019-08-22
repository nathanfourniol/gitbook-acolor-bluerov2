# Required configuration

## Hardware

According to the ArduSub project, the companion computer must be a Raspberry Pi 3 model B \(not B+\) to ensure complete support

## Software

The raspberry Pi need the companion computer image from BlueRobotics. You can find [here](https://www.ardusub.com/getting-started/installation.html#ardusub) how to install the latest image.

If you want to use the two additional IMUS, you can use the image _aColor-BlueRov2-raspberry-with-server-for-imu-4Gb.img_ that comes with all dependencies for the ROV and the IMUS.

## Internal Raspberry Pi system

### Processes running

At the start of the Raspberry Pi, few processes started : MAVproxy, a server for IMUs, processes for web interface.

### Access internal system

#### SSH

You can access Raspberry Pi internal system via SSH. There is no graphical desktop everything mus be do by command line or by the companion Web interface.

```text
ssh pi@192.168.2.2
```

The password is companion.

#### Companion Web interface

Companion computer hosts a web interface with useful different pages for accessing parameters and functionalities associated with Companion computer. See [https://www.ardusub.com/operators-manual/companion-web.html](https://www.ardusub.com/operators-manual/companion-web.html)

## More information

See [https://www.ardusub.com](https://www.ardusub.com)

