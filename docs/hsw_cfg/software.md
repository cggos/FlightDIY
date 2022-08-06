# Software

---

## 飞控 (FCU) 固件

- PX4 固件
    - 专为 **Pixhawk** 开发的固件。相对封闭，代码体系相对简单清晰，社区相对小，迭代慢一些，但因为相对清晰，适合学习研究。

* APM 固件
    - `arducopter4.0.7-px4.apj`
    - 专为 **Arduupilot** 开发的固件，现也用于PIXHAWK。有ArduCopter社区支撑、开放，功能全、迭代升级快，适合直接用。由于有较多的历史兼容性需求，软件代码体系相对杂乱，还封装了PX4的内核，学习起来困难些。

APM和PX4是两款不同开源飞控固件，均可以跑在Pixhawk这款硬件板上。


## 地面站 (GCS)

### APM: MissionPlanner (MP)

#### MP on Linux

- Mission Planner下载链接：[https://firmware.ardupilot.org/Tools/MissionPlanner/archive/](https://firmware.ardupilot.org/Tools/MissionPlanner/archive/)
    - 注意：最新版本连接飞控有些奇怪问题，**1.3.74** 版本测试是ok的，后面的都不太好用

- [https://ardupilot.org/planner/docs/mission-planner-installation.html#mission-planner-on-linux](https://ardupilot.org/planner/docs/mission-planner-installation.html#mission-planner-on-linux)
    - **QGC** and **MAVProxy** are alternatives that run stably in Linux


- run using **MONO**
  ```sh
  mono MissionPlanner.exe
  ```

### PX4: QGroundControl (QGC)

- [http://qgroundcontrol.com/](http://qgroundcontrol.com/)

- Ubuntu 18.04
    - [https://github.com/mavlink/qgroundcontrol/releases/download/v4.0.11/QGroundControl.AppImage](https://github.com/mavlink/qgroundcontrol/releases/download/v4.0.11/QGroundControl.AppImage)

    ```sh
    ./QGroundControl.AppImage
    ```
