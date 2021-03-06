## Overview
Xsens DOT Server is a simple web server that can scan, connect and start measurement with Xsens DOT. The system is built using Node.js in combination with [Noble](https://github.com/abandonware/noble). 

While you can get all measurement modes, 3 modes are supported in current Xsens DOT Server:
* Complete (Euler)
* Extended (Quaternion)
* Rate quantities (with mag)

Get more information about Xsens DOT in [Develepor Page](https://www.xsens.com/developer) and [Base](https://base.xsens.com/hc/en-us/categories/360002285079-Wearable-Sensor-Platform).

## Important Notices
Disconnect all Bluetooth peripherals (mouse, keyboard) before start Xsens DOT Server to ensure stable Bluetooth connections. 

## Documentation
* [System Architecture](documentation/XsensDOTServer-SystemArchitecture.pdf): system architecture of Xsens DOT Server.
* [Sensor Server](documentation/XsensDOTServer-SensorServer.pdf): application and workflow control.
* [BLE Handler](documentation/XsensDOTServer-BLEHandler.pdf): creates an abstraction from the BLE protocol.
* [Web GUI Handler](documentation/XsensDOTServer-WebGUIHandler.pdf): the web server
* [Noble](https://github.com/noble/noble): Node package that implements an interface with the BLE radio (i.e. driver).
* [Web Client](documentation/XsensDOTServerWebClient.pdf): a web browser that can run on any computer on the local network and that renders an HTML page that implements the GUI.

## Set up the environment
* [Windows](#set-up-on-windows)
* [Rasberry Pi](#set-up-on-raspberry-pi)
* [macOS](#set-up-on-macos)

### Set up on Windows
#### Prerequisites
* Windows 10, 64-bit
* Compatible Bluetooth 4.0 USB adapter or above

#### Install the following tools
* Install Python 3.8.3 from the [Micfrosoft Store package](https://docs.python.org/3/using/windows.html#the-microsoft-store-package) 
* Install [Node.js-v12.16.2-x64](https://nodejs.org/download/release/v12.16.2/node-v12.16.2-x64.msi)
  * Keep clicking **Next** to complete the installation.
  * Enter `npm -v` in command prompt to check if the installation is successful.<br>
&nbsp;<img height="60" src="images/image002.gif"/>

* Install [node-gyp](https://github.com/nodejs/node-gyp#installation)
   
   `npm install -g node-gyp`
* Install all the required tools and configurations using Microsoft's [windows-build-tools](https://github.com/felixrieseberg/windows-build-tools) from an elevated PowerShell or CMD.exe (run as Administrator)

  `npm install --global --production windows-build-tools`
* Install [Zadig](https://zadig.akeo.ie/) to setup WinUSB driver:
  * Find Bluetooth adapter inforamtion in Device Manager <br>
&nbsp;<img height="250" src="images/image006.gif"/>
  * Open Zadig, goto **Options**, enable "**List All Devices**"
  * Find your Bluetooth adapter, change the driver to **WinUSB**. Then click **Replace Driver** <br>
&nbsp;<img height="200" src="images/image007.gif"/>

  * Note: please retry several times if the intallation fails. Or restart the computer and try again. 

#### Troubleshooting
If you encounter `Error: No compatible USB Bluetooth 4.0 device found!` when try to run Xsens DOT Sever
 1. Find the VID and PID of your Bluetooth device<br>
&nbsp;<img height="300" src="images/image011.gif"/>
 2. Open source code: *XsensDOTserver\node_modules\bluetooth-hci-socket\lib\usb.js*
 3. Add Bluetooth VID & PID in usb.js (line 66)<br>
&nbsp;<img height="80" src="images/image012.gif"/>
 4. Run Xsens DOT Server again


### Set up on macOS
#### Install following tools
* Install [node.js 8.11.1](https://nodejs.org/download/release/v8.11.1/)

### Set up on Raspberry Pi
#### Prerequisites
* Raspberry Pi 4 Model B 4GB RAM
* Install [Raspberry Pi OS](https://www.raspberrypi.org/downloads/raspberry-pi-os/)

#### Installation steps
* Install dependcies
  
  ```sh
  sudo apt-get install bluetooth bluez libbluetooth-dev libudev-dev
  sudo apt-get install build-essential checkinstall libssl-dev
  ```

* Install node.js 8.11.1: 
  ```sh
  sudo apt-get install npm
  sudo npm cache clean -f
  sudo npm install -g -n
  sudo n 8.11.1
  node -v
  ```

## Run Xsens DOT Server
1. Clone repository
  
   `git clone https://github.com/xsens/xsens_dot_server.git`
1. Enter Xsens DOT Server project `cd ./xsens_dot_server` and install the dependency package `npm install`
1. Run Xsens DOT Server
   * Windows: `node xsensDotServer`
   * Raspberry Pi: `sudo node xsensDotServer`
1. Open Xsens DOT server in browser
   * Run http://localhost:8080/ and you are able to use Xsens DOT Server!

## Known issues
1. Unable to connect sensors in macOS.

## Bug reports and feedback
All feedback is welcome and helps us to improve!

Please report all bugs by [rasing an issue](https://github.com/xsens/xsens_dot_server/issues/new).

You can also discuss Xsens DOT related topics in our [Community Forum](https://base.xsens.com/hc/en-us/community/topics).


