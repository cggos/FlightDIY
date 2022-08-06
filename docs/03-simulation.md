# Simulation

* [ROS with Gazebo Simulation](https://docs.px4.io/main/en/simulation/ros_interface.html)

> Crashing simulated planes is a lot cheaper than crashing real ones!

---

<p align="center">
  <img src="/img/pc_mavros_fcu.png" style="width:80%">
</p>

仿真首先分为 **软件在环仿真 (SITL)** 和 **硬件在环仿真 (HITL)**。目前来看，软件在环仿真更简单实现及方便。

软件在环仿真一共是有 [jMAVSim](https://dev.px4.io/en/simulation/jmavsim.html)、[Gazebo](https://dev.px4.io/en/simulation/gazebo.html)、[AirSim](https://dev.px4.io/en/simulation/airsim.html) 这三种。jMAVSim 是一个轻量级的仿真器，目前只支持四旋翼仿真。Gazebo 支持旋翼、固定翼、倾转、小车等，是所有仿真器里支持平台最多的，也能支持多个无人机的仿真，在各个仿真器比较的表格里，PX4官方是这么说Gazebo仿真的: **This simulator is highly recommended**.

一般而言，如果我是修改了PX4固件内的代码，比如修改了姿态控制器，我会用 **jMAVSim** 调试，同时打开地面站，利用 **定点及自稳模式** 进行飞行测试，还能下载log看看记录的量对不对。jMAVSim不吃电脑配置，运行比较流畅，适合快速验证PX4内部代码逻辑及检查修改固件后的BUG。

如果我需要用到 px4_command 及 mavros包 来进行 offboard模式的测试，我会使用 **Gazebo** 仿真。比如我在机载电脑中修改了一些控制逻辑，打开Gazebo仿真，同时运行mavros及相应节点，将仿真的无人机切换至offboard模式，在Gazebo中测试我修改的代码是否正确，十分好用！

这只是个人的使用习惯，正常来讲，后面说的那个功能用jMAVSim也能做，但你既然都跑ROS了，肯定用一个和ROS相关的仿真器更加好用一点。jMAVSim比不过Gazebo的一点是它无法进行固定翼、小车的仿真，以及无法进行视觉类的仿真，无法修改飞行环境等等。



## Installing ROS and Gazebo

### Gazebo

```yaml
# ~/.ignition/fuel/config.yaml
servers:
  -
    name: osrf
    url: https://fuel.ignitionrobotics.org
```

### MAVROS

* [ROS with MAVROS Installation Guide](https://docs.px4.io/main/en/ros/mavros_installation.html)

[MAVROS](http://wiki.ros.org/mavros): **MAVLink** extendable communication node for ROS with proxy for Ground Control Station.

<p align="center">
  <img src="/img/mavros.png" style="width:80%">
  <img src="/img/mavlink.png" style="width:80%">
</p>


## Launching ROS/Simulation

```sh
roslaunch mavros px4.launch fcu_url:="udp://:14540@127.0.0.1:14557"
```

## Launching Gazebo with ROS Wrappers

- [PX4-Autopilot](https://github.com/PX4/PX4-Autopilot)

```sh
git clone https://github.com/PX4/PX4-Autopilot.git --recursive
```

### Gazebo Simulator

```sh
cd <PX4-Autopilot_clone>

make px4_sitl gazebo
make px4_sitl_default gazebo

# or
DONT_RUN=1 make px4_sitl_default gazebo
source ~/catkin_ws/devel/setup.bash    # (optional)
source Tools/setup_gazebo.bash $(pwd) $(pwd)/build/px4_sitl_default
export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:$(pwd)
export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:$(pwd)/Tools/sitl_gazebo
roslaunch px4 posix_sitl.launch
```

启动成功后，会看到Gazebo中有一个iris无人机。这时你可以打开QGC地面站，地面站会默认连接这台飞机，你可以尝试利用地面站发送起飞指令测试。

### jMAVSim Simulator

```sh
cd <PX4-Autopilot_clone>

make px4_sitl jmavsim
```


## Control & Output

### GCS

```sh
./QGroundControl.AppImage
```

### Output

```sh
rostopic echo /mavros/imu/data
rostopic list
```
