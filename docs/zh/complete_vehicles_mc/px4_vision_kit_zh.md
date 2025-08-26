# PX4 Vision 自主开发套件

[_PX4 Vision 自主开发套件_](https://holybro.com/collections/multicopter-kit/PX4-Vision) 是一个坚固且经济实惠的套件，用于在自主飞行器上进行计算机视觉开发。

![概述](../../assets/hardware/px4_vision_devkit/px4_vision_v1.5_front.png)

该套件包含一个接近即飞的碳纤维四轴飞行器，配备了 _Pixhawk 4_ 或 _Pixhawk 6C_（V1.5版本）飞控、一个 _UP Core_ 伴随计算机（4GB 内存和 64GB eMMC），以及一个 Occipital _Structure Core_ 深度摄像头传感器。

本指南解释了使飞行器准备飞行所需的最少额外设置（安装遥控系统和电池）。它还涵盖了首次飞行以及如何开始修改计算机视觉代码。

:::warning
PX4 不再支持本文档中描述的避障软件：

- [PX4/PX4-Avoidance](https://github.com/PX4/PX4-Avoidance) 已存档
- [路径规划接口](../computer_vision/path_planning_interface.md)，以及任务中的避障和安全着陆。

套件中包含一个 USB 存储器，其中包含基于此软件的避障功能实现示例。
此示例仅用作参考，用于演示平台的功能。
:::

::: tip
此套件仍然强烈推荐用于开发和测试视觉解决方案（不依赖于传统集成）。
:::

## 购买渠道

- [PX4 Vision Dev Kit v1.5](https://holybro.com/collections/multicopter-kit/products/px4-vision-dev-kit-v1-5)
- [PX4 Vision Dev Kit v1 (已停产)](https://holybro.com/collections/multicopter-kit/products/px4-vision)

## Px4 Vision 指南内容

- [警告和通知](#warnings-and-notifications)
- [套件内容](#what-is-inside)
- [您还需要什么](#what-else-do-you-need)
- [首次设置](#first-time-setup)
- [使用避障功能飞行无人机](#fly-the-drone-with-avoidance)
- [使用套件进行开发](#development-using-the-kit)
- [PX4 Vision 载板引脚分布](#px4-vision-carrier-board-pinouts)
- [其他开发资源](#other-development-resources)
- [如何获得技术支持](#how-to-get-technical-support)

## 警告和通知

1. 该套件适用于使用前向摄像头的计算机视觉项目（它没有向下或向后的深度摄像头）。
   因此，它不能（不经修改）用于测试需要向下摄像头的功能。
1. 任务中的避障只能在GPS可用时测试（任务使用GPS坐标）。
   碰撞防护可以在位置模式下测试，前提是来自GPS或光流的位置锁定良好。
1. 标有 `USB1` 的端口在与 _USB3_ 外设一起使用时可能会干扰 GPS（禁用依赖GPS的功能，包括任务）。
   这就是为什么启动镜像在 _USB2.0_ 存储器上提供的原因。
1. PX4 Vision v1 的 ECN 010 或以上版本（载板 RC05 及以上），_UP Core_ 可以由 DC 插头或电池供电。

   ![RC 编号](../../assets/hardware/px4_vision_devkit/rc.png) ![ECN 编号](../../assets/hardware/px4_vision_devkit/serial_number_update.jpg)

1. 所有 PX4 Vision v1.5 _UP Core_ 都可以由 DC 插头或电池供电。

:::warning
对于 ECN 低于 010/载板低于 RC04 的 PX4 Vision v1，_UP Core_ 应该只使用电池供电（不要拆下 _UP Core 电源_ 插座安全罩）。这不适用于 PX4 Vision v1.5

![警告 - 不要连接电源端口](../../assets/hardware/px4_vision_devkit/warning_power_port_update.png)
:::

## 套件内容

::: info
PX4 Vision V1 和 V1.5 之间的区别可以在 [这里](https://docs.holybro.com/drone-development-kit/px4-vision-dev-kit-v1.5/v1-and-v1.5-difference) 找到
:::

![PV4 Vision v1.5](../../assets/hardware/px4_vision_devkit/px4_vision_v1.5_whats_inside.jpg)

PX4 Vision V1 的内容可以在 [PX4 v1.13 文档](https://docs.px4.io/v1.13/en/complete_vehicles/px4_vision_kit.html#what-is-inside) 中找到。

PX4 Vision 开发套件包含以下组件：

- 核心组件：
  - 1x Pixhawk 4 或 Pixhawk 6C（v1.5版本）飞控
  - 1x PMW3901 光流传感器
  - 1x TOF 红外距离传感器（PSK‐CM8JL65‐CC5）
  - 1x Structure Core 深度摄像头
    - 160 度广角视觉摄像头
    - 立体红外摄像头
    - 机载 IMU
    - 强大的 NU3000 多核深度处理器
  - 1x _UP Core_ 计算机（4GB 内存和 64GB eMMC，预装 Ubuntu 和 PX4 避障）
    - Intel® Atom™ x5-z8350（最高 1.92 GHz）
    - 兼容操作系统：Microsoft Windows 10 完整版、Linux（ubilinux、Ubuntu、Yocto）、Android
    - FTDI UART 连接到飞控
    - `USB1`：USB3.0 A 端口，用于从 USB2.0 存储器启动 PX4 避障环境（连接 USB3.0 外设可能会干扰 GPS）。
    - `USB2`：JST-GH 连接器上的 USB2.0 端口。可用于第二个摄像头、LTE等（或在开发过程中用于键盘/鼠标）。
    - `USB3`：连接到深度摄像头的 USB2.0 JST-GH 端口
    - `HDMI`：HDMI 输出
    - SD 卡插槽
    - WiFi 802.11 b/g/n @ 2.4 GHz（连接到外部天线 #1）。允许计算机访问家庭 WiFi 网络进行互联网访问/更新。

- 机械规格：
  - 机架：全 5mm 3k 碳纤维斜纹
  - 电机：T-MOTOR KV1750
  - ESC：BEHEli-S 20A ESC
  - GPS：M8N GPS 模块
  - 电源模块：Holybro PM07
  - 轴距：286mm
  - 重量：不含电池或螺旋桨 854 克
  - 遥测：ESP8266 连接到飞控（连接到外部天线 #2）。实现与地面站的无线连接。

- 一个 USB2.0 存储器，预刷写软件包：
  - Ubuntu 18.04 LTS
  - ROS Melodic
  - Occipital Structure Core ROS 驱动程序
  - MAVROS
  - [PX4 Avoidance](https://github.com/PX4/PX4-Avoidance)

- 各种电缆、8个螺旋桨、2个电池带（已安装）和其他配件（这些可用于连接其他外设）。

## 您还需要什么

套件包含除电池和无线电控制系统以外的所有基本无人机硬件，这些必须单独购买：

- 电池：
  - 带 XT60 母头连接器的 4S LiPo
  - 长度小于 115mm（以适合电源连接器和 GPS 桅杆之间）
- 无线电控制系统
  - 可以使用任何 [PX4兼容的遥控系统](../getting_started/rc_transmitter_receiver.md)。
  - _FrSky Taranis_ 发射机配 R-XSR 接收机是更受欢迎的设置之一。
- H2.0 内六角扳手（用于拧开顶板以便连接遥控接收机）

此外，用户需要地面站硬件/软件：

- 运行 [QGroundControl](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/getting_started/download_and_install.html)（QGC）的笔记本电脑或平板电脑。

## 首次设置

1. 将 [兼容的遥控接收机](../getting_started/rc_transmitter_receiver.md#connecting-receivers) 连接到飞行器（套件不包含）：
   - 使用 H2.0 内六角扳手拆下/拧开顶板（放电池的地方）。
   - [将接收机连接到飞控](../assembly/quick_start_pixhawk4.md#radio-control)。
   - 重新装上顶板。
   - 将遥控接收机安装在飞行器后部的 _UP Core_ 载板上（使用扎带或双面胶带）。
   - 确保天线远离任何障碍物并与机架电气隔离（例如将它们固定在载板下方或飞行器臂或腿上）。

1. [绑定](../getting_started/rc_transmitter_receiver.md#binding) 遥控地面和空中单元（如果尚未完成）。
   绑定程序取决于使用的具体无线电系统（阅读接收机手册）。
1. 将 GPS 桅杆升至垂直位置，并将盖子拧到基板上的固定器上。（v1.5 不需要）

   ![升起 GPS 桅杆](../../assets/hardware/px4_vision_devkit/raise_gps_mast.jpg)

1. 将套件中的预制镜像 USB2.0 存储器插入标有 `USB1` 的 _UP Core_ 端口（如下所示）。

   ![UP Core: USB1 端口](../../assets/hardware/px4_vision_devkit/upcore_port_usb1.png)

1. 使用充满电的电池为飞行器供电。
   ::: info
   在连接电池之前确保已拆下螺旋桨。
   :::
1. 使用以下默认凭据将地面站连接到飞行器 WiFi 网络（几秒钟后）：
   - **SSID：** pixhawk4
   - **密码：** pixhawk4

   :::tip
   连接后，可以通过使用网络浏览器打开 URL：`http://192.168.4.1` 来更改 WiFi 网络 SSID、密码和其他凭据（如果需要）。
   波特率不得从 921600 更改。
   :::

1. 在地面站上启动 _QGroundControl_。
1. [配置/校准](../config/index.md) 飞行器：

   ::: info
   飞行器应该预先校准（例如固件、机架、电池和传感器都已设置）。
   但是，您需要校准无线电系统（您刚刚连接的），重新进行指南针校准通常也是值得的。
   :::
   - [校准无线电系统](../config/radio.md)
   - [校准指南针](../config/compass.md)

1. （可选）在遥控器上配置 [飞行模式选择开关](../config/flight_mode.md)。

   ::: info
   模式也可以使用 _QGroundControl_ 更改
   :::

   我们建议为遥控器开关定义：
   - [位置模式](../flight_modes_mc/position.md) - 可用于测试碰撞防护的安全手动飞行模式。
   - [任务模式](../flight_modes_mc/mission.md) - 运行任务并测试避障。
   - [返航模式](../flight_modes_mc/return.md) - 将飞行器安全返回到起飞点并着陆。

1. 按照所示旋转方向安装螺旋桨：

   ![电机顺序图](../../assets/hardware/px4_vision_devkit/motor_order_diagram.png)
   - 螺旋桨方向可以从标签确定：_6045_（正常，逆时针）和 _6045_**R**（反向，顺时针）。

     ![螺旋桨识别](../../assets/hardware/px4_vision_devkit/propeller_directions.jpg)

   - 使用提供的螺旋桨螺母牢固拧紧：

     ![螺旋桨螺母](../../assets/hardware/px4_vision_devkit/propeller_nuts.png)

## 使用避障功能飞行无人机

当上述飞行器设置完成时：

1. 连接电池为飞行器供电。

1. 等待启动序列完成并且避障系统启动（飞行器在启动期间将拒绝解锁命令）。

   :::tip
   从提供的 USB 存储器启动/启动过程大约需要 1 分钟（或从 [内部存储器](#install_image_mission_computer) 30 秒）。
   :::

1. 检查避障系统是否正确启动：
   - _QGroundControl_ 通知日志显示消息：**Avoidance system connected**。

     ![QGC 日志显示避障系统已启动](../../assets/hardware/px4_vision_devkit/qgc_console_vision_system_started.jpg)

   - _Structure Core_ 摄像头前面有红色激光可见。

1. 等待 GPS LED 变绿。
   这意味着飞行器有 GPS 定位并准备飞行！
1. 将地面站连接到飞行器 WiFi 网络。
1. 找到一个安全的户外飞行地点，理想情况下有一棵树或其他方便的障碍物来测试 PX4 Vision。

1. 要测试 [碰撞防护](../computer_vision/collision_prevention.md)，启用 [位置模式](../flight_modes_mc/position.md) 并手动飞向障碍物。
   飞行器应该减速，然后在距离障碍物 6m 内停止（距离可以使用 [CP_DIST](../advanced_config/parameter_reference.md#CP_DIST) 参数 [更改](../advanced_config/parameters.md)）。

1. 要测试避障，创建一个路径被障碍物阻挡的任务。
   然后切换到 [任务模式](../flight_modes_mc/mission.md) 运行任务，观察飞行器绕过障碍物然后返回计划航线。

## 使用套件进行开发

以下部分解释了如何使用该套件作为开发计算机视觉软件的环境。

### PX4 Avoidance 概述

:::warning
此功能不再 [被 PX4 支持](../computer_vision/path_planning_interface.md)。
:::

_PX4 Avoidance_ 系统由在伴随计算机（连接深度摄像头）上运行的计算机视觉软件组成，该软件向运行在 _飞控_ 上的 PX4 飞行堆栈提供障碍物和/或路线信息。

关于伴随计算机视觉/规划软件的文档可以在 github 上找到：[PX4/PX4-Avoidance](https://github.com/PX4/PX4-Avoidance)。
该项目提供了多种不同的规划器实现（打包为 ROS 节点）：

- PX4 Vision 套件默认运行 _localplanner_，这是您自己软件的推荐起点。
- _globalplanner_ 尚未与此套件测试。
- _landing planner_ 需要向下摄像头，在不首先修改摄像头安装的情况下无法使用。

PX4 和伴随计算机通过 [MAVLink](https://mavlink.io/en/) 使用以下接口交换数据：

- [路径规划接口](../computer_vision/path_planning_interface.md) - 用于在自动模式中实现避障功能的 API。
- [碰撞防护接口](../computer_vision/collision_prevention.md) - 用于基于障碍物地图在手动位置模式中进行基于飞行器的避障的 API（目前用于碰撞防护）。

<a id="install_image_mission_computer"></a>

### 在伴随计算机上安装镜像

您可以在 _UP Core_ 上安装镜像并从内部存储器启动（而不是 USB 存储器）。

推荐这样做，因为从内部存储器启动要快得多，释放了一个 USB 端口，并且可能提供比您的 USB 存储器更多的内存。

::: info
从内部存储器启动大约需要 30 秒，而从提供的 USB2 存储器启动大约需要一分钟（其他卡可能需要几倍的时间）。
:::

要将 USB 镜像刷写到 _UP Core_：

1. 将预刷写的 USB 驱动器插入标有 `USB1` 的 _UP Core_ 端口。
1. [登录到伴随计算机](#login_mission_computer)（如上所述）。
1. 打开终端并运行以下命令将镜像复制到内部存储器（eMMC）。
   终端将在刷写过程中提示多个响应。

   ```sh
   cd ~/catkin_ws/src/px4vision_ros/tools
   sudo ./flash_emmc.sh
   ```

   ::: info
   执行此脚本时，_UP Core_ 计算机中保存的所有信息都将被删除。
   :::

1. 拔出 USB 存储器。
1. 重启飞行器。
   _UP Core_ 计算机现在将从内部存储器（eMMC）启动。

### 启动伴随计算机

首先将提供的 USB2.0 存储器插入标有 `USB1` 的 _UP Core_ 端口，然后使用 4S 电池为飞行器供电。
避障系统应该在大约 1 分钟内启动（尽管这确实取决于提供的 USB 存储器）。

:::tip
[使用避障功能飞行无人机](#fly-the-drone-with-avoidance) 额外解释了如何验证避障系统是否激活。
:::

如果您已经 [在伴随计算机上安装了镜像](#install_image_mission_computer)，您只需为飞行器供电即可（即不需要 USB 存储器）。
避障系统应该在大约 30 秒内启动并运行。

一旦启动，伴随计算机就可以用作计算机视觉开发环境和运行软件。

<a id="login_mission_computer"></a>

### 登录到伴随计算机

要登录到伴随计算机：

1. 通过端口 `USB2` 将键盘和鼠标连接到 _UP Core_：

   ![UP Core: USB2](../../assets/hardware/px4_vision_devkit/upcore_port_usb2.png)
   - 使用套件中的 USB-JST 电缆获得 USB A 连接器

     ![USB 转 JST 电缆](../../assets/hardware/px4_vision_devkit/usb_jst_cable.jpg)

   - 如果键盘和鼠标有单独的连接器，可以将 USB 集线器连接到电缆。

1. 将显示器连接到 _UP Core_ HDMI 端口。

   ![UP Core: HDMI 端口](../../assets/hardware/px4_vision_devkit/upcore_port_hdmi.png)

   Ubuntu 登录屏幕应该会在显示器上出现。

1. 使用凭据登录到 _UP Core_：
   - **用户名：** px4vision
   - **密码：** px4vision

### 开发/扩展 PX4 Avoidance

PX4 Vision 的 _UP Core_ 计算机提供了一个完整且完全配置的环境，用于扩展 PX4 Avoidance 软件（更一般地说，用于使用 ROS 2 开发新的计算机视觉算法）。
您应该在飞行器上开发和测试您的软件，将其同步到您自己的 git 仓库，并在 github [PX4/PX4-Avoidance](https://github.com/PX4/PX4-Avoidance) 仓库上与更广泛的 PX4 社区共享任何修复和改进。

catkin 工作空间位于 `~/catkin_ws`，并预配置为运行 PX4 避障本地规划器。
启动文件 (`avoidance.launch`) 位于 `px4vision_ros` 包中（修改此文件以更改启动的规划器）。

避障包在启动时启动。
要集成不同的规划器，需要禁用此功能。

1. 使用以下命令禁用避障进程：

   ```sh
   systemctl stop avoidance.service
   ```

   您可以简单地重启机器来重启服务。

   其他有用的命令是：

   ```sh
   # 重启服务
   systemctl start avoidance.service

   # 禁用服务（停止服务并在启动后不重启）
   systemctl disable avoidance.service

   # 启用服务（启动服务并在启动后启用重启）
   systemctl enable avoidance.service
   ```

1. 避障包的源代码可以在 https://github.com/PX4/PX4-Avoidance 找到，该仓库位于 `~/catkin_ws/src/avoidance`。

1. 对代码进行更改！要获取避障的最新代码，请从避障仓库拉取代码：

   ```sh
   git pull origin
   git checkout origin/master
   ```

1. 构建包

   ```sh
   catkin build local_planner
   ```

ROS 工作空间位于 `~/catkin_ws`。
有关在 ROS 中开发和使用 catkin 工作空间的参考，请参阅 [ROS catkin 教程](https://wiki.ros.org/catkin/Tutorials)。

### 开发 PX4 固件

您可以修改 PX4 本身，并 [将其安装为自定义固件](../config/firmware.md#custom)：

- 您需要 **通过 USB** 将 _QGroundControl_ 连接到套件的 _Pixhawk_ 以更新固件。
- 加载新固件后选择 _PX4 Vision DevKit_ 机架：
  ![机架选择 - PX4 Vision DevKit](../../assets/hardware/px4_vision_devkit/qgc_airframe_px4_vision_devkit_platform.jpg)

## PX4 Vision 载板引脚分布

PX4 Vision 1.15 的信息可以在 [https://docs.holybro.com](https://docs.holybro.com/drone-development-kit/px4-vision-dev-kit-v1.5) 找到。
载板引脚分布和其他信息在 [下载部分](https://docs.holybro.com/drone-development-kit/px4-vision-dev-kit-v1.5/downloads)。

## 其他开发资源

- [_UP Core_ Wiki](https://github.com/up-board/up-community/wiki/Ubuntu) - _Up Core_ 伴随计算机技术信息
- [Occipital 开发者论坛](https://structure.io/developers/) - _Structure Core_ 摄像头信息
- [Pixhawk 4 概述](../flight_controller/pixhawk4.md)
- [Pixhawk 6C 概述](../flight_controller/pixhawk6c.md)

## 如何获得技术支持

对于硬件问题，请联系 Holybro：[productservice@holybro.com](mailto:productservice@holybro.com)。

对于软件问题，请使用以下社区支持渠道：

- [Holybro PX4 Vision Wikifactory](https://wikifactory.com/+holybro/px4-vision)
- [PX4 支持渠道](../contribute/support.md)
