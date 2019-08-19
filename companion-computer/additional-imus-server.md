# Additional IMUs server

## Connection

The two additional IMUs are connected to Rasberry Pi in I2C.

### Instruction for connecting IMUs in I2C 

## Server

To send data to topside computer, a server is launched when the Rasbperry start. This server read data from IMUs. To collect data on topside computer, you should launch the Imu\_brigde.py . It is a client to the server running on Raspberry Pi.

### Server configuration

|  |  |
| ---: | :--- |
| IP | 192.168.2.2 |
| Port | 14600 |

