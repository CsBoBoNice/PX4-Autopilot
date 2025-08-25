# Hex Cube Black 飞行控制器

:::warning
PX4 不制造此产品（或任何其他自动驾驶仪）。
如有硬件支持或合规问题，请联系[制造商](https://cubepilot.org/#/home)。
:::

:::tip
[Cube Orange](cubepilot_cube_orange.md) 是本产品的继任者。
但是，我们建议考虑基于行业标准构建的产品，例如 [Pixhawk 标准](autopilot_pixhawk_standard.md)。
此飞行控制器不遵循标准，使用的是专利连接器。
:::

[Hex Cube Black](https://docs.cubepilot.org/user-guides/autopilot/the-cube) 飞行控制器（以前称为 Pixhawk 2.1）是一款灵活的自动驾驶仪，主要面向商业系统制造商。
它基于 [Pixhawk项目](https://pixhawk.org/) **FMUv3** 开放硬件设计，在 [NuttX](https://nuttx.apache.org/) 操作系统上运行 PX4。

![Cube Black](../../assets/flight_controller/cube/cube_black_hero.png)

该控制器设计为与特定领域的载板一起使用，以减少布线，提高可靠性并便于组装。
例如，商业检测车辆的载板可能包括与伴随计算机的连接，
而赛车载板可能包括来自车辆框架的电调。

Cube 在两个 IMU 上包含振动隔离，第三个固定 IMU 作为参考/备份。

::: info
制造商的 [Cube 用户指南](https://docs.cubepilot.org/user-guides/autopilot/the-cube) 包含详细信息，包括 [Cube 颜色差异概述](https://docs.cubepilot.org/user-guides/autopilot/the-cube/introduction/specifications)。
:::

:::tip
此自动驾驶仪由 PX4 维护和测试团队[支持](../flight_controller/autopilot_pixhawk_standard.md)。
:::

## 主要特征

- 32位 STM32F427 [Cortex-M4F](https://en.wikipedia.org/wiki/ARM_Cortex-M#Cortex-M4)<sup>&reg;</sup> 内核，带 FPU
- 168 MHz / 252 MIPS
- 256 KB RAM
- 2 MB Flash（完全可访问）
- 32位 STM32F103 故障安全协处理器
- 14 路 PWM / 舵机输出（8 路带故障安全和手动覆盖，6 路辅助，高功率兼容）
- 丰富的附加外设连接选项（UART、I2C、CAN）
- 集成的飞行中恢复和手动覆盖备份系统，带专用处理器和独立电源（固定翼使用）
- 备份系统集成混合功能，提供一致的自动驾驶仪和手动覆盖混合模式（固定翼使用）
- 冗余电源输入和自动故障转移
- 外部安全开关
- 多色 LED 主视觉指示器
- 高功率、多音调压电音频指示器
- microSD 卡，用于长时间高速率日志记录

<a id="stores"></a>

## 购买地点

[Cube Black](https://www.cubepilot.com/#/reseller/list)（经销商列表）

## 组装

[Cube 接线快速入门](../assembly/quick_start_cube.md)

## 规格

### 处理器

- 32位 STM32F427 [Cortex M4](https://en.wikipedia.org/wiki/ARM_Cortex-M#Cortex-M4) 内核，带 FPU
- 168 MHz / 252 MIPS
- 256 KB RAM
- 2 MB Flash（完全可访问）
- 32位 STM32F103 故障安全协处理器

### 传感器

- 待定

### 接口

- 5x UART（串口），一个高功率，2个带硬件流控制
- 2x CAN（一个带内部 3.3V 收发器，一个在扩展连接器上）
- Spektrum DSM / DSM2 / DSM-X® 卫星兼容输入
- Futaba S.BUS® 兼容输入和输出
- PPM 总和信号输入
- RSSI（PWM 或电压）输入
- I2C
- SPI
- 3.3v ADC 输入
- 内部 microUSB 端口和外部 microUSB 端口扩展

### 电源系统和保护

- 带自动故障转移的理想二极管控制器
- 舵机导轨高功率（最大 10V）和大电流（10A+）就绪
- 所有外设输出过流保护，所有输入 ESD 保护

### 电压额定值

如果提供三个电源，Pixhawk 可以在电源上实现三重冗余。三个导轨是：电源模块输入、舵机导轨输入、USB 输入。

#### 正常操作最大额定值

在这些条件下，所有电源将按此顺序用于为系统供电

- 电源模块输入（4.8V 至 5.4V）
- 舵机导轨输入（4.8V 至 5.4V）**手动覆盖最高 10V，但如果电源模块输入不存在，自动驾驶仪部分在 5.7V 以上将断电**
- USB 电源输入（4.8V 至 5.4V）

#### 绝对最大额定值

在这些条件下，系统不会汲取任何电力（不会运行），但将保持完整。

- 电源模块输入（4.1V 至 5.7V，0V 至 20V 不损坏）
- 舵机导轨输入（4.1V 至 5.7V，0V 至 20V）
- USB 电源输入（4.1V 至 5.7V，0V 至 6V）

## 引脚图和原理图

板原理图和其他文档可以在这里找到：[The Cube Project](https://github.com/proficnc/The-Cube)。

## 端口

### 顶部（GPS、TELEM 等）

![Cube 端口 - 顶部（GPS、TELEM 等）和主/辅助](../../assets/flight_controller/cube/cube_ports_top_main.jpg)

<a id="serial_ports"></a>

### 串口映射

| UART   | Device     | Port                  |
| ------ | ---------- | --------------------- |
| USART1 | /dev/ttyS0 | <!-- IO debug? -->    |
| USART2 | /dev/ttyS1 | TELEM1（流控制）       |
| USART3 | /dev/ttyS2 | TELEM2（流控制）       |
| UART4  | /dev/ttyS3 | GPS1                  |
| USART6 | /dev/ttyS4 | PX4IO                 |
| UART7  | /dev/ttyS5 | CONSOLE               |
| UART8  | /dev/ttyS6 | <!-- unknown -->      |

<!-- Note: Got ports using https://github.com/PX4/PX4-user_guide/pull/672#issuecomment-598198434 -->
<!-- This originally said " **TEL4:** /dev/ttyS6 (ttyS4 UART):  **Note** `TEL4` is labeled as `GPS2` on Cube." -->

### 调试端口

![Cube 调试端口](../../assets/flight_controller/cube/cube_ports_debug.jpg)

### USB/SD卡端口

![Cube USB/SD卡端口](../../assets/flight_controller/cube/cube_ports_usb_sdcard.jpg)

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，_QGroundControl_ 会自动安装。
:::

要为此目标[构建 PX4](../dev_setup/building_px4.md)：

```
make px4_fmu-v3_default
```

## 问题

Cube Black 上的 CAN1 和 CAN2 丝印标记是颠倒的（CAN1 是 CAN2，反之亦然）。

## 更多信息/文档

- [Cube 接线快速入门](../assembly/quick_start_cube.md)
- Cube 文档（制造商）：
  - [Cube 用户指南](https://docs.cubepilot.org/user-guides/autopilot/the-cube)
  - [Mini 载板](https://docs.cubepilot.org/user-guides/carrier-boards/mini-carrier-board)
