---
description: description of the gui.py and BlueRov2.ui
---

# Graphical User Interface \(GUI\)

## Graphical aspect

![](../.gitbook/assets/guiinaction.png)

### Description of the GUI

{% tabs %}
{% tab title="STATUS" %}
![](../.gitbook/assets/guiinactionstatus.png)

| Components | Description |
| ---: | :--- |
| ARM/DISARM | Show the arm status of the BlueRov2 |
| Control | MANUAL : ROV controlled by gamepad  AUTOMATIC : ROV controlled by the depth/heading/velocity controllers   |
| enable AUTOMATIC control | Allow to enable AUTOMATIC mode without a gamepad |
| Battery Level | Display battery level in volt \(to not damage the battery it is recommend to not go under 3V by cells : e.g. for a 4S LI-Ion battery do not go under 12V\)  |
| Light level | light level of the lights in %, 0: turned off, 100% : highest brightness |
| Camera | Camera angle : between -45 to 45 deg |
{% endtab %}

{% tab title="SET PARAMETERS" %}
![](../.gitbook/assets/guiinactionset_params.png)

<table>
  <thead>
    <tr>
      <th style="text-align:right">Components</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:right">Set target</td>
      <td style="text-align:left">
        <p>Depth : in m, 1m = 1m depth</p>
        <p>Heading : in deg, 0 is North</p>
        <p>Velocity : in m/s (the controller is not working)</p>
        <p>SEND : publish on /Settings/set_target</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:right">PWM MAX</td>
      <td style="text-align:left">
        <p>Set the pwm maximal for <b>all</b> controllers. Uses in saturation method
          in controllers.</p>
        <p>At the init the pwm maximal is 1700</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:right">PID parameters</td>
      <td style="text-align:left">
        <p>To tune PID for each controller. Press SEND for each controller to change
          PID parameters. The message is sent on the topics /Settings/set_[depth/heading/velocity].</p>
        <p>KI, KP, KD = integral, proportional, derivative coefficients</p>
        <p><b>Note :</b> heading and velocity controller have no KI, changing this
          parameter will have no effect.</p>
      </td>
    </tr>
  </tbody>
</table>
{% endtab %}

{% tab title="RECORD DATA" %}
![](../.gitbook/assets/guiinactionrecord_data.png)

This area allows to record data by launching a rosbag record command described below. You can change the record time, in s, up to 3600s. The record time from Start All button is the maximum of the three record time parameters.

The files are recorded in **~/.ros** folder. Rosbag file will be named as  
\[depth/heading/velocity\]\[year\]-\[month\]-\[day\]-\[hours\]-\[minutes\]-\[seconds\].bag

| Choice | Topics recorded |
| :--- | :--- |
| Depth | /BlueRov2/bar30 ; /BlueRov2/state ;  /Settings/set\_depth ; /Settings/set\_target ; /Command/depth |
| Heading |  /BlueRov2/imu/attitude ; /BlueRov2/state ; /Settings/set\_heading ; /Settings/set\_target ; /Command/heading |
| Velocity | /imu/imu\_raw ; /BlueRov2/state ; /Settings/set\_velocity ; /Settings/set\_target ; /Command/velocity |
| All | /BlueRov2/bar30 ; /BlueRov2/imu/attitude ; /imu/imu\_raw ; /BlueRov2/state ; /Settings/set\_depth ; /Settings/set\_heading ; /Settings/set\_velocity ; /Settings/set\_target ; /Command/depth ; /Command/heading ; /Command/velocity |

{% hint style="info" %}
The velocity is not recorded as velocity but only acceleration are recorded with the topics /imu/data\_raw
{% endhint %}
{% endtab %}

{% tab title="CONTROLLER OVERVIEW" %}
![](../.gitbook/assets/guiinactionctrl_overview.png)

It's an overview of the controllers with a preview of the controllers output in the column PWM\_sent. The checkbox can be check to enable the controller to drive the ROV if the AUTOMATIC mode otherwise it will not work until the AUTOMATIC mode is on.

Units are meters for altitude \(eg : 0.174m=0.174m above the surface\), degrees for heading in range 0-360, velocity is not estimated yet so is always written -1. See here [velocity control](controllers/velocity-control.md).
{% endtab %}
{% endtabs %}

## Features

### Record data

### Enable controller

## ROS

### Node

GUI

### Topics

| ROS message subscribed | Message | Description |
| :---: | :---: | :--- |
| /BlueRov2/State | bluerov\_ros\_playground/State |  |
| /BlueRov2/battery | sensor\_msgs/BatteryState |  |
| /BlueRov2/bar30 | bluerov\_ros\_playground/Bar30 |  |
| /BlueRov2/imu/attitude | bluerov\_ros\_playground/Attitude |  |
| /Command/depth | UInt16 |  |
| /Command/heading | UInt16 |  |
| /Command/velocity | UInt16 |  |
| /Command/velocity | UInt16 |  |
| /Settings/set\_depth | bluerov\_ros\_playground/Set\_depth |  |
| /Settings/set\_heading | bluerov\_ros\_playground/Set\_heading |  |
| /Settings/set\_velocity | bluerov\_ros\_playground/Set\_velocity |  |
| /Settings/set\_target | bluerov\_ros\_playground/Set\_target |  |

| ROS message published | Message | Description |
| :---: | :---: | :--- |
| /Settings/set\_depth | bluerov\_ros\_playground/Set\_depth |  |
| /Settings/set\_heading | bluerov\_ros\_playground/Set\_heading |  |
| /Settings/set\_velocity | bluerov\_ros\_playground/Set\_velocity |  |
| /Settings/set\_target | bluerov\_ros\_playground/Set\_target |  |

