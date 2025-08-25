# Pixhawk 3 Pro（已停产）

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](https://store-drotek.com/)获取硬件支持或合规问题。
:::

Pixhawk<sup>&reg;</sup> 3 Pro基于FMUv4硬件设计（Pixracer），带有一些升级和附加功能。
该板由[Drotek<sup>&reg;</sup>](https://drotek.com)和PX4设计。

![Pixhawk 3 Pro主图](../../assets/hardware/hardware-pixhawk3_pro.jpg)

::: info
主要硬件文档在这里：https://drotek.gitbook.io/pixhawk-3-pro/hardware
:::

:::tip
此自动驾驶仪由PX4维护和测试团队[支持](../flight_controller/autopilot_pixhawk_standard.md)。
:::

## 快速摘要

- 微控制器：**STM32F469**；闪存大小为**2MiB**，RAM大小为**384KiB**
- **ICM-20608-G**陀螺仪/加速度计
- **MPU-9250**陀螺仪/加速度计/磁力计
- **LIS3MDL**指南针
- 传感器通过两个SPI总线连接（一个高速率和一个低噪音总线）
- 两个I2C总线
- 两个CAN总线
- 来自两个电源模块的电压/电池读数
- FrSky<sup>&reg;</sup>反相器
- 8个主PWM + 6个辅助PWM输出（独立IO芯片，PX4IO）
- microSD（日志记录）
- S.BUS / Spektrum / SUMD / PPM输入
- JST GH用户友好连接器：与Pixracer相同的连接器和引脚排列

## 购买地点

不再可用。

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，会由_QGroundControl_自动安装。
:::

要为此目标[构建PX4](../dev_setup/building_px4.md)：

```
make px4_fmu-v4pro_default
```

## 调试端口

该板有FMU和IO调试端口，如下所示。

![调试端口](../../assets/flight_controller/pixhawk3pro/pixhawk3_pro_debug_ports.jpg)

引脚排列和连接器符合[Pixhawk连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)中定义的[Pixhawk调试迷你](../debug/swd_debug.md#pixhawk-debug-mini)接口（JST SM06B连接器）。

| 引脚    | 信号             | 电压  |
| ------- | ---------------- | ----- |
| 1（红） | VCC TARGET SHIFT | +3.3V |
| 2（黑） | CONSOLE TX（OUT）| +3.3V |
| 3（黑） | CONSOLE RX（IN） | +3.3V |
| 4（黑） | SWDIO            | +3.3V |
| 5（黑） | SWCLK            | +3.3V |
| 6（黑） | GND              | GND   |

有关接线和使用此端口的信息，请参见：

- [SWD调试端口](../debug/swd_debug.md)
- [PX4系统控制台](../debug/system_console.md#pixhawk_debug_port)（注意，FMU控制台映射到UART7）。

## 串口映射

| UART   | 设备       | 端口                  |
| ------ | ---------- | --------------------- |
| UART1  | /dev/ttyS0 | WiFi                  |
| USART2 | /dev/ttyS1 | TELEM1（流控制）      |
| USART3 | /dev/ttyS2 | TELEM2（流控制）      |
| UART4  |            |
| UART7  | CONSOLE    |
| UART8  | SERIAL4    |

<!-- Note: Got ports using https://github.com/PX4/PX4-user_guide/pull/672#issuecomment-598198434 -->
