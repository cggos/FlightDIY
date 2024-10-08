# Development PX4

- https://px4.io/
- https://docs.px4.io/main/
- https://dronecode.org/

---

## Overview

* https://px4.io/software/getting-started/hello-sky/ubuntu/


## Flight Review

- [Flight Review](https://logs.px4.io/)


## Download & Install

download

```bash
git clone https://github.com/PX4/PX4-Autopilot.git --recursive
```

install

```bash
bash Tools/setup/ubuntu.sh
```

list

```bash
make list_config_targets
```

## First Build (Using the jMAVSim Simulator)

```bash
make distclean

make px4_sitl jmavsim
```

```bash
pxh> commander takeoff

pxh> commander land
```

## First Application Tutorial (Hello Sky)

```bash
make distclean

make px4_fmu-v5_default [upload]
```

output

```
[0/13] Performing build step for 'px4io_firmware'
ninja: no work to do.
[1/2] uploading px4
Loaded firmware for board id: 50,0 size: 1892041 bytes (91.65%), waiting for the bootloader...

Attempting reboot on /dev/serial/by-id/usb-ArduPilot_Pixhawk4_2A003D000550304E35313320-if02 with baudrate=57600...
If the board does not respond, unplug and re-plug the USB connector.

Found board id: 50,0 bootloader version: 5 on /dev/serial/by-id/usb-3D_Robotics_PX4_BL_FMU_v5.x_0-if00
sn: 003d002a4e30500520333135
chip: 10016451
family: b'STM32F7[6|7]x'
revision: b'Z'
flash: 2064384 bytes
Windowed mode: False

Erase  : [====================] 100.0%
Program: [====================] 100.0%
Verify : [====================] 100.0%
Rebooting. Elapsed Time 26.817
```

## MAVROS Offboard control example

- [MAVROS Offboard control example (C++)](https://docs.px4.io/main/en/ros/mavros_offboard_cpp.html)

```bash
rosrun px4_sim offb_node
```

## NSH控制台

> 拔掉SD卡（脚本中提到的没有SD卡进入nsh，有SD时进入MAVLINK，因此会出现一段乱码）

```bash
./Tools/mavlink_shell.py /dev/ttyACM0

# or: PX4 Toolchain->TeraTerm (Windows)

# or
screen /dev/ttyAVM0 57600 8N1

# or 
sudo minicom
```

output

```
Using port /dev/serial/by-id/usb-3D_Robotics_PX4_FMU_v5.x_0-if00
Connecting to MAVLINK...

NuttShell (NSH) NuttX-10.2.0
nsh>
nsh> px4_simple_app
INFO  [px4_simple_app] Hello Sky!
INFO  [px4_simple_app] Accelerometer:	 -0.0865	 -0.1489	 -9.8105
INFO  [px4_simple_app] Accelerometer:	 -0.0839	 -0.1436	 -9.8115
INFO  [px4_simple_app] Accelerometer:	 -0.0911	 -0.1582	 -9.8103
INFO  [px4_simple_app] Accelerometer:	 -0.1014	 -0.1553	 -9.8027
INFO  [px4_simple_app] Accelerometer:	 -0.0836	 -0.1614	 -9.8154
INFO  [px4_simple_app] exiting
```
