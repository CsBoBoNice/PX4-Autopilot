# mRo-X2.1自动驾驶仪（已停产）

<Badge type="info" text="已停产" /> <!-- 202507 / PX4v1.16 -->

:::warning
此飞行控制器已[停产](../flight_controller/autopilot_experimental.md)，不再有商业销售。
:::

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](https://store.mrobotics.io/)获取硬件支持或合规问题。
:::

[mRo-X2.1自动驾驶仪](http://www.mRobotics.io/)基于[Pixhawk<sup>&reg;</sup>项目](https://pixhawk.org/) **FMUv2**开源硬件设计。
它在[NuttX](https://nuttx.apache.org/) OS上运行PX4。

![mRo X2.1](../../assets/flight_controller/mro/mro_x2.1.jpg)

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 快速摘要

- 主系统芯片：[STM32F427](https://www.st.com/en/microcontrollers-microprocessors/stm32f427-437.html)
  - CPU：STM32F427VIT6 ARM<sup>&reg;</sup>微控制器 - 版本3
  - IO：STM32F100C8T6 ARM<sup>&reg;</sup>微控制器
- 传感器：
  - Invensense<sup>&reg;</sup> MPU9250 9DOF
  - Invensense ICM-20602 6DOF
  - MEAS MS5611气压计
- 尺寸/重量
  - 尺寸：36mm x 50mm
    （可订购垂直、水平或无引脚安装）
  - 安装点：30.5mm x 30.5mm 3.2mm直径
  - 重量：10.9g

下图提供了与Pixhawk 1的并排比较。
mRo具有几乎相同的硬件和连接性，但
占用空间要小得多。
主要区别是更新的传感器和Rev 3 FMU。

![Mro Pixhawk 1 vs X2.1比较](../../assets/flight_controller/mro/px1_x21.jpg)

## 连接性

- 2.54mm引脚：
- GPS（UART4）带I2C
- CAN总线
- RC输入
- PPM输入
- Spektrum输入
- RSSI输入
- sBus输入
- sBus输出
- 电源输入
- 蜂鸣器输出
- LED输出
- 8个舵机输出
- 6个辅助输出
- 板外microUSB连接器
- Kill Pin输出_（目前固件不支持）_
- 空速传感器
- USART2（Telem 1）
- USART3（Telem 2）
- UART7（控制台）
- UART8（OSD）

## PX4引导加载程序问题

默认情况下，mRo X2.1可能预配置为ArduPilot<sup>&reg;</sup>而不是PX4。这
可以在固件更新期间看到，当板被识别为FMUv2而不是X2.1时。

在这种情况下，您必须使用[BL_Update_X21.zip](https://github.com/PX4/PX4-Autopilot/raw/main/docs/assets/hardware/BL_Update_X21.zip)更新引导加载程序。
如果不进行此纠正，您的指南针方向将是错误的，并且
不会检测到辅助IMU。

更新步骤如下：

1. 下载并解压[BL_Update_X21.zip](https://github.com/PX4/PX4-Autopilot/raw/main/docs/assets/hardware/BL_Update_X21.zip)。
2. 找到文件夹_BL_Update_X21_。这包含一个**bin**文件和一个名为**/etc**的子文件夹，其中包含一个**rc.txt**文件
3. 将这些文件复制到您的microSD卡的根目录并将其插入mRO x2.1
4. 打开mRO x2.1，等待它启动，然后重启1次。

## 可用性

此产品可在[mRobotics<sup>&reg;</sup>商店](https://store.mrobotics.io/mRo-X2-1-Rev-2-p/m10021a.htm)订购。

## 接线指南

![mRo_X2.1_Wiring](../../assets/flight_controller/mro/mro_x21_wiring.png)

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，会由_QGroundControl_自动安装。
:::

要为此目标[构建PX4](../dev_setup/building_px4.md)：

```
make mro_x21_default
```

## 原理图

该板在mRo硬件仓库中有文档：[x21_V2_schematic.pdf](https://github.com/mRoboticsIO/Hardware/blob/master/X2.1/Docs/x21_V2_schematic.pdf)。

## 串口映射

| UART   | 设备       | 端口            |
| ------ | ---------- | --------------- |
| USART1 | /dev/ttyS0 | IO调试          |
| USART2 | /dev/ttyS1 | SERIAL1         |
| USART3 | /dev/ttyS2 | TELEM2          |
| UART4  | /dev/ttyS3 | GPS/I2C         |
| USART6 | /dev/ttyS4 | PX4IO           |
| UART7  | /dev/ttyS5 | SERIAL5控制台   |
| UART8  | /dev/ttyS6 | SERIAL4         |

<!-- Note: Got ports using https://github.com/PX4/PX4-user_guide/pull/672#issuecomment-598198434 -->
