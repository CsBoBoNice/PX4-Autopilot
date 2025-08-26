# 罗盘校准

此过程校准和配置所有[磁力计](../gps_compass/index.md)。
_QGroundControl_ 将指导您将飞行器定位在多个设定方向并围绕指定轴旋转飞行器。

::: info
它还自动检测外部磁力计的罗盘方向（[默认](../advanced_config/parameter_reference.md#SENS_MAG_AUTOROT)）。
如果您已经[安装罗盘](../assembly/mount_gps_compass.md#compass-orientation)在非标准角度，您需要在校准前[手动设置罗盘方向](../config/flight_controller_orientation.md#setting-the-compass-orientation)。
:::

## 概述

当您首次设置飞行器时需要校准罗盘，如果飞行器曾经暴露在非常强的磁场中，或在具有异常磁特性的区域使用，可能需要重新校准。

:::tip
糟糕的罗盘校准的迹象包括多旋翼在悬停期间盘旋、"抽水马桶"现象（以增大半径盘旋/螺旋向外，通常保持恒定高度，导致飞走），或在尝试直线飞行时偏离路径。
_QGroundControl_ 也应该通知错误 `mag sensors inconsistent`。
:::

该过程校准所有罗盘并自动检测任何外部罗盘的方向。
如果有任何外部磁力计可用，它将禁用内部磁力计（这些主要用于外部磁力计的自动旋转检测）。

有几种类型的罗盘校准可用：

1. [完整](#complete-calibration)：首次在机架上安装自动驾驶仪或当飞行器配置发生重大变化时需要此校准。
   它通过估计每个轴的偏移和比例因子来补偿硬铁和软铁效应。
1. [部分](#partial-quick-calibration)：在准备飞行器飞行时、更换载荷后或罗盘玫瑰看起来不准确时，可以进行此校准作为例行程序。
   这种类型的校准只估计偏移以补偿硬铁效应。
1. [大型飞行器](#large-vehicle-calibration)：当飞行器太大或太重无法进行完整校准时可以进行此校准。这种类型的校准只估计偏移以补偿硬铁效应。

## 执行校准

### 先决条件

开始校准前：

1. 选择远离大型金属物体或磁场的位置。
   :::tip
   金属并不总是显而易见的！避免在办公桌上校准（经常包含金属条）或在车辆旁边校准。
   如果您站在钢筋分布不均匀的混凝土板上，校准甚至可能受到影响。
   :::
1. 如果可能，通过遥测无线电而不是USB连接。
   USB可能造成显著的磁干扰。
1. 如果使用外部罗盘（或组合GPS/罗盘模块），确保将其[安装](../assembly/mount_gps_compass.md)尽可能远离其他电子设备以减少磁干扰，并保持_支持的方向_。

### 完整校准

校准步骤如下：

1. 启动 _QGroundControl_ 并连接飞行器。
1. 选择**"Q"图标 > 飞行器设置 > 传感器**（侧边栏）打开_传感器设置_。
1. 点击**罗盘**传感器按钮。

   ![选择罗盘校准PX4](../../assets/qgc/setup/sensor/sensor_compass_select_px4.png)

   ::: info
   您应该已经设置了[自动驾驶仪方向](../config/flight_controller_orientation.md)。如果没有，您也可以在这里设置。
   :::

1. 点击**确定**开始校准。
1. 将飞行器放置在显示为红色（未完成）的任何方向并保持静止。一旦提示（方向图像变为黄色），围绕指定轴在任一/两个方向旋转飞行器。一旦当前方向的校准完成，屏幕上相关的图像将变为绿色。

   ![PX4上的罗盘校准步骤](../../assets/qgc/setup/sensor/sensor_compass_calibrate_px4.png)

1. 对所有飞行器方向重复校准过程。

一旦您在所有位置校准了飞行器，_QGroundControl_ 将显示_校准完成_（所有方向图像将显示为绿色，进度条将完全填满）。然后您可以继续下一个传感器。

### 部分"快速"校准

此校准类似于智能手机上众所周知的8字形罗盘校准：

1. 将飞行器拿在您面前，随机在所有轴上执行部分旋转。
   在每个方向上2-3次约30度的振荡通常就足够了。
1. 等待航向估计稳定并验证罗盘玫瑰指向正确方向（这可能需要几秒钟）。

注意：

- 此类型的校准没有开始/停止（当飞行器解锁时算法连续运行）。
- 校准立即应用于数据（无需重启），但仅在飞行器解锁后保存到校准参数（如果在校准和关机之间没有执行解锁/上锁序列，校准将丢失）。
- 步骤1中部分旋转的幅度和速度会影响校准质量。
  遵循上述建议通常就足够了。

### 大型飞行器校准

<Badge type="tip" text="PX4 v1.15" />

此校准过程利用飞行器方向和位置的外部知识，以及世界磁模型（WMM）来校准硬铁偏差。

1. 确保GNSS定位。这是在WMM表中找到预期地磁场所必需的。
2. 将飞行器对齐面向真北。
   为了获得最佳结果，请尽可能准确。
3. 打开[QGroundControl MAVLink控制台](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/analyze_view/mavlink_console.html)并发送以下命令：

   ```sh
   commander calibrate mag quick
   ```

注意：

- 此方法专门为完全旋转不切实际或不可能的飞行器设计。
  如果可以完全旋转，请使用[完整校准](#complete-calibration)。
- 飞行器不需要完全水平，因为这会使用倾斜估计自动补偿。
- 此校准也可以使用MAVLink命令[MAV_CMD_FIXED_MAG_CAL_YAW](https://mavlink.io/en/messages/common.html#MAV_CMD_FIXED_MAG_CAL_YAW)触发。

## 验证

校准完成后，检查航向指示器和地图上箭头的航向是否稳定并与飞行器方向匹配，例如将其转向基本方向时。

## 额外校准/配置

上述过程将自动检测、[设置默认旋转](../advanced_config/parameter_reference.md#SENS_MAG_AUTOROT)、校准和优先排序所有可用磁力计。
如果有外部磁力计可用，内部磁力计将被禁用。

通常不需要进一步的罗盘配置。

### 启用/禁用罗盘

虽然不应该_需要_进一步配置，但希望出于任何原因（如测试）禁用/启用罗盘的开发人员可以使用罗盘参数来完成。
这些参数以[CAL*MAGx*](../advanced_config/parameter_reference.md#CAL_MAG0_ID)为前缀（其中 `x=0-3`）：

- [CAL_MAGn_ROT](../advanced_config/parameter_reference.md#CAL_MAG0_ROT)可用于确定哪些罗盘是内部的。
  如果`CAL_MAGn_ROT==1`，罗盘是内部的。
- [CAL_MAGx_PRIO](../advanced_config/parameter_reference.md#CAL_MAG0_PRIO)设置相对罗盘优先级，可用于禁用罗盘。

## 调试

通过设置[SDLOG_MODE=1](../advanced_config/parameter_reference.md#SDLOG_MODE)和[SDLOG_PROFILE=64](../advanced_config/parameter_reference.md#SDLOG_PROFILE)，可以记录磁力计（实际上是所有传感器）的原始比较数据。
有关更多信息，请参见[日志记录](../dev_log/logging.md)。

## 更多信息

- [外设 > GPS & 罗盘](../gps_compass/index.md)
- [基本组装](../assembly/index.md)（每个飞行控制器的设置指南）
- [罗盘功率补偿](../advanced_config/compass_power_compensation.md)（高级配置）
- [QGroundControl用户指南 > 传感器](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/sensors_px4.html#compass)
- [PX4设置视频 - @2m38s](https://youtu.be/91VGmdSlbo4?t=2m38s) (Youtube)
