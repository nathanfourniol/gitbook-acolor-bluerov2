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
      </td>
    </tr>
  </tbody>
</table>
{% endtab %}

{% tab title="RECORD DATA" %}
![](../.gitbook/assets/guiinactionrecord_data.png)
{% endtab %}

{% tab title="CONTROLLER OVERVIEW" %}
![](../.gitbook/assets/guiinactionctrl_overview.png)
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

