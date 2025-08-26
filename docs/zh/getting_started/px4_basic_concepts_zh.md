# 基本概念

本主题提供了无人机和使用 PX4 的基本介绍（主要面向新手用户，但对于更有经验的用户也是很好的介绍）。

如果您已经熟悉基本概念，可以继续阅读[基本组装](../assembly/index.md)来学习如何连接您特定的自动驾驶仪硬件。
要加载固件并使用 _QGroundControl_ 设置飞行器，请参见[基本配置](../config/index.md)。

## 什么是无人机？

无人机，或无人飞行器（UV），是一种可以手动或自主控制的无人"机器人"飞行器。
它们可以在空中、地面、水面/水下移动，被用于许多[消费、工业、政府和军事应用](https://px4.io/ecosystem/commercial-systems/)，包括航空摄影/录像、运输货物、竞速、搜索和测量等。

无人机更正式地被称为无人飞行器（UAV）、无人地面车辆（UGV）、无人水面车辆（USV）、无人水下车辆（UUV）。

::: info
无人飞行器系统（UAS）一词通常指 UAV 以及完整系统的所有其他组件，包括地面控制站和/或无线电控制器，以及用于控制无人机、捕获和处理数据的任何其他系统。
:::

## 无人机类型

有许多不同的飞行器机架（类型），在每种类型中都有许多变化。
下面列出了一些类型，以及它们最适合的使用案例。

- [多旋翼](../frames_multicopter/index.md) — 多旋翼飞行器提供精确悬停和垂直起飞，但代价是飞行时间较短且通常速度较慢。
  它们是最受欢迎的飞行器类型，部分原因是它们易于组装，而且 PX4 有使它们易于飞行且非常适合作为相机平台的模式。
- [直升机](../frames_helicopter/index.md) — 直升机具有与多旋翼相似的优势，但机械上更复杂，效率更高。
  它们也更难飞行。
- [飞机（固定翼）](../frames_plane/index.md) — 固定翼飞行器比多旋翼提供更长、更快的飞行，因此更适合地面测量等应用。
  但是，它们比多旋翼更难飞行和着陆，如果您需要悬停或飞得很慢（例如，测量垂直结构时）则不适合。
- [VTOL](../frames_vtol/index.md)（垂直起降）- 混合固定翼/多旋翼飞行器提供两全其美：像多旋翼一样在垂直模式下起飞和悬停，但像飞机一样过渡到前飞以覆盖更多地面。
  VTOL 通常比多旋翼和固定翼飞机更昂贵，更难构建和调试。
  它们有多种类型：倾转旋翼机、尾座机、四平面等。
- [飞艇](../frames_airship/index.md)/[气球](../frames_balloon/index.md) — 轻于空气的飞行器，通常提供高空长时间飞行，代价是对飞行速度和方向的控制有限（或没有）。
- [漫游者](../frames_rover/index.md) — 类似汽车的地面车辆。
  它们控制简单，通常使用起来很有趣。
  它们不能像大多数飞机那样快速移动，但可以携带更重的载荷，在静止时不消耗太多电力。
- **船只** — 水面车辆。
- [潜水器](../frames_sub/index.md) — 水下车辆。

更多信息请参见：

- [飞行器类型和设置](../airframes/index.md)
- [机架设置](../config/airframe.md)
- [机架参考](../airframes/airframe_reference.md)。

## 自动驾驶仪

无人机的"大脑"被称为自动驾驶仪。

它最少包括运行在 _飞行控制器_（FC）硬件上的实时操作系统（"RTOS"）上的 _飞行栈_ 软件。
飞行栈提供基本的稳定性和安全功能，通常还为手动飞行提供一定程度的飞行员辅助，并自动化常见任务，如起飞、着陆和执行预定义任务。

一些自动驾驶仪还包括一个通用计算系统，可以提供"更高级别"的指挥和控制，并支持更先进的网络、计算机视觉和其他功能。
这可能作为单独的[伴随计算机](#offboard-companion-computer)实现，但在未来越来越可能成为完全集成的组件。

## PX4 飞行栈

[PX4](https://px4.io/) 是在 NuttX RTOS 上运行的强大开源自动驾驶仪 _飞行栈_。

PX4 的一些关键特性包括：

- 支持许多不同的飞行器机架/类型，包括：[多旋翼](../frames_multicopter/index.md)、[固定翼飞机](../frames_plane/index.md)（飞机）、[VTOL](../frames_vtol/index.md)（混合多旋翼/固定翼）、[地面车辆](../frames_rover/index.md)和[水下车辆](../frames_sub/index.md)。
- 为[飞行控制器](#flight-controller)、[传感器](#sensors)、[载荷](#payloads)和其他外设提供无人机组件的绝佳选择。
- 灵活强大的[飞行模式](#flight-modes)和[安全功能](#safety-settings-failsafe)。
- 与[伴随计算机](#offboard-companion-computer)和[机器人 API](../robotics/index.md)（如 [ROS 2](../ros2/user_guide.md) 和 [MAVSDK](https://mavsdk.mavlink.io/main/en/index.html)）的强大深度集成。

PX4 是更广泛的无人机平台的核心部分，该平台包括 [QGroundControl](#qgc) 地面站、[Pixhawk 硬件](https://pixhawk.org/)，以及用于与伴随计算机、相机和其他使用 MAVLink 协议的硬件集成的 [MAVSDK](https://mavsdk.mavlink.io/main/en/index.html)。
PX4 由 [Dronecode 项目](https://dronecode.org/) 支持。

## 地面控制站

地面控制站（GCS）是基于地面的系统，允许 UV 操作员监控和控制无人机及其载荷。
下面列出了已知与 PX4 配合使用的产品子集。

### QGroundControl {#qgc}

Dronecode GCS 软件称为 [QGroundControl](https://qgroundcontrol.com/)（"QGC"）。
它在 Windows、Android、MacOS 或 Linux 硬件上运行，支持各种屏幕尺寸。
您可以从[这里](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/getting_started/download_and_install.html)下载它（免费）。

![QGC 主屏幕](../../assets/concepts/qgc_fly_view.png)

QGroundControl 使用遥测无线电（双向数据链路）与无人机通信，允许您获得实时飞行和安全信息，并使用点击界面控制飞行器、相机和其他载荷。
在支持的硬件上，您还可以使用操纵杆控制器手动飞行飞行器。
QGC 还可用于可视化规划、执行和监控自主任务、设置地理围栏等。

QGroundControl 桌面版本还用于安装（刷写）PX4 固件并在无人机的自动驾驶仪/飞行控制器硬件上配置 PX4。

### Auterion Mission Control (AMC) {#amc}

[Auterion Mission Control](https://auterion.com/product/mission-control/) 是一个功能强大且功能齐全的地面控制站应用程序，针对 _飞行员_ 而非飞行器配置进行了优化。
虽然设计用于与 Auterion 产品配合使用，但也可以与"原版"PX4 一起使用。

更多信息请参见：

- [AMC 文档](https://docs.auterion.com/vehicle-operation/auterion-mission-control)
- [从 Auterion Suite 下载](https://suite.auterion.com/)

## 无人机组件和部件

### 飞行控制器

飞行控制器（FC）是加载和运行 PX4 飞行栈固件的硬件。
它们连接到传感器，PX4 从传感器确定其状态，以及连接到执行器/电机，PX4 使用它们来稳定和移动飞行器。

<img src="../../assets/flight_controller/cuav_pixhawk_v6x/pixhawk_v6x.jpg" width="230px" title="CUAV Pixhawk 6X" >

PX4 可以在许多不同类型的[飞行控制器硬件](../flight_controller/index.md)上运行，从 [Pixhawk 系列](../flight_controller/pixhawk_series.md)控制器到 Linux 计算机。
这些包括 [Pixhawk 标准](../flight_controller/autopilot_pixhawk_standard.md)和[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)的板子。
您应该选择适合您飞行器物理约束、您希望执行的活动和成本的板子。

更多信息请参见：[飞行控制器选择](flight_controller_selection.md)

### 传感器

PX4 使用传感器来确定飞行器状态，稳定飞行器和启用自主控制需要这些状态。
飞行器状态包括：位置/高度、航向、速度、空速、方向（姿态）、不同轴的旋转速率、电池电量等。

PX4 _最少需要_[陀螺仪](../sensor/gyroscope.md)、[加速度计](../sensor/accelerometer.md)、[磁力计](../gps_compass/magnetometer.md)（指南针）和[气压计](../sensor/barometer.md)。
这组最小传感器集成在 [Pixhawk 系列](../flight_controller/pixhawk_series.md)飞行控制器中（也可能在其他控制器平台中）。

可以将其他/外部传感器连接到控制器。
建议使用以下传感器：

- 需要 [GNSS/GPS](../gps_compass/index.md) 或其他全球位置源来启用所有自动模式和一些手动/辅助模式。

  通常使用结合 GNSS 和指南针的模块，因为外部指南针相比飞行控制器中的内部指南针不太容易受到电磁干扰。

- 强烈建议固定翼和 VTOL 飞行器使用[空速传感器](../sensor/airspeed.md)。
- 强烈建议所有飞行器类型使用[距离传感器（测距仪）](../sensor/rangefinders.md)，因为它们允许更平滑、更稳健的着陆，并在多旋翼上启用地形跟随等功能。
- [光流传感器](../sensor/optical_flow.md)可与多旋翼和 VTOL 上的距离传感器一起使用，以支持 GNSS 拒绝环境中的导航。

有关传感器的更多信息，请参见：[传感器硬件和设置](../sensor/index.md)。

### 输出：电机、舵机、执行器

PX4 使用 _输出_ 来控制：电机速度（例如通过 [ESC](#escs-motors)）、飞行表面如副翼和襟翼、相机触发器、降落伞、抓手和许多其他类型的载荷。

输出可能是 PWM 端口或 DroneCAN 节点（例如 DroneCAN [电机控制器](../dronecan/escs.md)）。
下图显示了 [Pixhawk 4](../flight_controller/pixhawk4.md) 和 [Pixhawk 4 mini](../flight_controller/pixhawk4_mini.md) 的 PWM 输出端口。

![Pixhawk 4 输出端口](../../assets/flight_controller/pixhawk4/pixhawk4_main_aux_ports.jpg) ![Pixhawk4 mini MAIN 端口](../../assets/flight_controller/pixhawk4mini/pixhawk4mini_pwm.png)

输出分为 `MAIN` 和 `AUX` 输出，并单独编号（即 `MAINn` 和 `AUXn`，其中 `n` 通常为 1 到 6 或 8）。
它们也可能标记为 `IO PWM Out` 和 `FMU PWM OUT`（或类似）。

:::warning
飞行控制器可能只有 `MAIN` PWM 输出（如 _Pixhawk 4 Mini_），或者 `MAIN` 或 `AUX` 上可能只有 6 个输出。
确保您选择的控制器有足够的端口/输出用于您的[机架](../airframes/airframe_reference.md)。
:::

您可以通过在 QGroundControl 中将相关功能（"Motor 1"）分配给所需输出（"AUX1"）来将几乎任何输出连接到任何电机或其他执行器：[执行器配置和测试](../config/actuators.md)。
请注意，每个机架的功能（电机和控制表面执行器位置）在[机架参考](../airframes/airframe_reference.md)中给出。

**注意：**

- Pixhawk 控制器有一个 FMU 板，_可能_ 有一个单独的 IO 板。
  如果有 IO 板，`AUX` 端口直接连接到 FMU，`MAIN` 端口连接到 IO 板。
  否则，`MAIN` 端口连接到 FMU，没有 `AUX` 端口。
- FMU 输出端口可以使用 [D-shot](../peripherals/dshot.md) 或 _One-shot_ 协议（以及 PWM），这提供了更低的延迟行为。
  这对竞速机和其他需要更好性能的机架很有用。
- `MAIN` 和 `AUX` 中只有 6-8 个输出，因为大多数飞行控制器只有这么多 PWM/Dshot/Oneshot 输出。
  理论上，如果总线支持，可以有更多输出（即 UAVCAN 总线不限制于这么少的节点）。

### ESC 和电机

许多 PX4 无人机使用无刷电机，这些电机由飞行控制器通过电子调速器（ESC）驱动
（ESC 将来自飞行控制器的信号转换为传递给电机的适当功率电平）。

有关 PX4 支持的 ESC/电机的信息，请参见：

- [ESC 和电机](../peripherals/esc_motors.md)
- [ESC 校准](../advanced_config/esc_calibration.md)
- [ESC 固件和协议概述](https://oscarliang.com/esc-firmware-protocols/)（oscarliang.com）

### 电池/电源

PX4 无人机通常由锂聚合物（LiPo）电池供电。
电池通常使用[电源模块](../power_module/index.md)或 _电源管理板_ 连接到系统，为飞行控制器和 ESC（用于电机）提供单独的电源。

有关电池和电池配置的信息可以在[电池估计调优](../config/battery.md)和[基本组装](../assembly/index.md)中的指南中找到（例如 [Pixhawk 4 接线快速入门 > 电源](../assembly/quick_start_pixhawk4.md#power)）。

### 手动控制

飞行员可以使用[无线电控制（RC）系统](../getting_started/rc_transmitter_receiver.md)或通过 QGroundControl 连接的[操纵杆/游戏手柄](../config/joystick.md)控制器手动控制飞行器。

![Taranis X9D 发射器](../../assets/hardware/transmitters/frsky_taranis_x9d_transmitter.jpg) <img src="../../assets/peripherals/joystick/micronav.jpg" alt="带有集成操纵杆的地面控制器 MicroNav 的照片" width="400px">

RC 系统使用专用的地面无线电发射器和基于飞行器的接收器来发送控制信息。
在首次调试/测试新机架设计时，或在飞行竞速机/特技飞行时（以及在低延迟很重要的其他情况下），应始终使用它们。

操纵杆系统使用 QGroundControl 将来自"标准"计算机游戏操纵杆的控制信息编码为 MAVLink 消息，并使用（共享）遥测无线电通道将其发送到飞行器。
只要您的遥测通道有足够高的带宽/低延迟，它们就可以用于大多数手动飞行用例，如起飞、测量等。

操纵杆通常用于集成 GCS/手动控制系统，因为集成操纵杆比单独的无线电系统更便宜、更容易，而且对于大多数用例，较低的延迟并不重要。
它们也非常适合飞行 PX4 模拟器，因为您可以将它们直接插入地面控制计算机。

::: info
PX4 在自主飞行模式下 _不需要_ 手动控制系统。
:::

## 飞行模式

模式是提供不同类型/级别的飞行器自动化和自动驾驶仪辅助的特殊操作状态。

_自主模式_ 完全由自动驾驶仪控制，不需要飞行员/遥控输入。
例如，这些用于自动化常见任务，如起飞、返回原点和着陆。
其他自主模式执行预编程任务、跟随 GPS 信标或接受来自机载计算机或地面站的命令。

_手动模式_ 由用户（通过 RC 控制杆/操纵杆）控制，并得到自动驾驶仪的辅助。
不同的手动模式提供不同的飞行特性 - 例如，一些模式启用特技飞行，
而其他模式不可能翻转，并会在风中保持位置/航线。

实现的飞行模式概述：

- [飞行模式（多旋翼）](../flight_modes_mc/index.md)
- [飞行模式（固定翼）](../flight_modes_fw/index.md)
- [飞行模式（VTOL）](../flight_modes_vtol/index.md)
- [驾驶模式（漫游者）](../flight_modes_rover/index.md)

## 安全设置（故障安全）

PX4 有可配置的故障安全系统来保护和恢复您的飞行器！
这些允许您指定可以安全飞行的区域和条件，以及如果触发故障安全将执行的操作（例如，着陆、保持位置或返回指定点）。

主要故障安全区域包括：

- 低电量
- 遥控（RC）丢失
- 位置丢失（全球位置估计质量太低）
- 机载丢失（例如与伴随计算机断开连接）
- 数据链路丢失（例如与 GCS 断开遥测连接）
- 地理围栏违反（限制飞行器在虚拟圆柱内飞行）

更多信息请参见：[安全](../config/safety.md)（基本配置）。

## 航向和方向

所有飞行器、船只和飞机都有基于其前进運动的航向方向或定向。

![Frame Heading](../../assets/concepts/frame_heading.png)

::: info
对于 VTOL 尾坐机，航向相对于多旋翼配置（即起飞、悬停、着陆期间的飞行器姿态）。
:::

了解飞行器航向方向很重要，以便将自动驾驶仪与飞行器移动矢量对齐。
多旋翼即使在所有方向上都对称，也有航向！
通常制造商使用彩色螺旋桦或彩色机臂来指示航向。

![Frame Heading TOP](../../assets/concepts/frame_heading_top.png)

在我们的图示中，我们将使用红色为多旋翼的前螺旋桦着色来显示航向。

您可以在[飞行控制器方向](../config/flight_controller_orientation.md)中深入了解航向。
