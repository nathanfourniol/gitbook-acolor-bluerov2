---
description: Description of the file server.py from Raspberry Py
---

# Additional IMUs : server

The two additional IMUs are connected to Rasberry Pi in I2C. If you have flashed the SD card with the image : _aColor-BlueRov2-raspberry-with-server-for-imu-4Gb.img_ the only thing do do is connecting the two IMUs to the Raspberry

### Connect IMUs on the Raspberry :

| Raspberry Pin | Sensor Pin |
| ---: | :--- |
| 3V3 | VIN |
| GND | GND |
| SCL | SCL |
| SDA | SDA |
| GND | SDOM \(only for the second IMU\) |
| GND | SDOAG \(only for the second IMU\) |

{% hint style="info" %}
To connect the two adafruit LSM9D1 IMUs on the same I2C bus, one of them must have its SDOM and SDOAG pin connected to the ground
{% endhint %}

### Libraries

{% hint style="info" %}
This is already setup in the _aColor-BlueRov2-raspberry-with-server-for-imu-4Gb.img_ 
{% endhint %}

This require Python3 and pip.

```text
sudo apt-get update
sudo apt-get upgrade
        
sudo apt-get python-smbus
sudo apt-get i2c-tools
        
pip3 install RPi.GPIO #a sudo may be necessary
pip3 install --upgrade setuptools #a sudo may be necessary
pip3 install adafruit-circuitpython-lsm9ds1 #a sudo may be necessary
```

In order to deal with the two IMUs on the same I2C bus we must replace the _adafruit\_lsm9ds1.py_ file in _/usr/local/lib/python3.4/dist-packages/_ by the file _adafruit\_lsm9ds1.py_ from the folder _tools/lib2imus/_ in the folder [_imu\_i2c_](../topside-computer/ros-architecture-and-file-system.md#file-system)_._ You can use the command in Raspberry Pi terminal

```text
sudo cp ~/imu_i2c/lib2imus/adafruit_lsm9ds1.py /usr/local/lib/python3.4/dist-packages/
```

## Server

To send data to topside computer, a server is launched when the Raspberry start. This server read data from IMUs. To collect data on topside computer, you should launch the client wich is the file Imu\_brigde.py. It is a client to the server running on Raspberry Pi.

### Server configuration

|  |  |
| ---: | :--- |
| IP | 192.168.2.2 |
| Port | 14600 |

