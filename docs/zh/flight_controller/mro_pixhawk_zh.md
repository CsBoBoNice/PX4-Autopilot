# mRo Pixhawk飞行控制器（Pixhawk 1）

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](https://store.mrobotics.io/)获取硬件支持或合规问题。
:::

_mRo Pixhawk<sup>&reg;</sup>_是原始[Pixhawk 1](../flight_controller/pixhawk.md)的硬件兼容版本。它在[NuttX](https://nuttx.apache.org/) OS上运行PX4。

:::tip
该控制器可以作为3DR<sup>&reg;</sup> [Pixhawk 1](../flight_controller/pixhawk.md)的直接替代品。
主要区别在于它基于[Pixhawk项目](https://pixhawk.org/) **FMUv3**开源硬件设计，该设计修正了一个将原始Pixhawk 1限制为1MB闪存的错误。
:::

![mRo Pixhawk图像](../../assets/flight_controller/mro/mro_pixhawk.jpg)

与PX4一起使用的组装/设置说明在此提供：[Pixhawk接线快速入门](../assembly/quick_start_pixhawk.md)

:::tip
此自动驾驶仪由PX4维护和测试团队[支持](../flight_controller/autopilot_pixhawk_standard.md)。
:::

## 主要特性

- 微处理器：
  - 32位STM32F427 Cortex<sup>&reg;</sup> M4核心，带FPU
  - 168 MHz/256 KB RAM/2 MB闪存
  - 32位STM32F100故障安全协处理器
  - 24 MHz/8 KB RAM/64 KB闪存
- 传感器：
  - ST Micro L3GD20 3轴16位陀螺仪
  - ST Micro LSM303D 3轴14位加速度计/磁力计
  - Invensense<sup>&reg;</sup> MPU 6000 3轴加速度计/陀螺仪
  - MEAS MS5611气压计
- 接口：
  - 5个UART（串口），一个高功率能力，2个带硬件流控制
  - 2个CAN
  - Spektrum DSM / DSM2 / DSM-X®卫星兼容输入，最高支持DX8（不支持DX9及以上）
  - Futaba<sup>&reg;</sup> S.BUS兼容输入和输出
  - PPM和信号
  - RSSI（PWM或电压）输入
  - I2C
  - SPI
  - 3.3和6.6V ADC输入
  - 外部microUSB端口
- 电源系统：
  - 理想二极管控制器，带自动故障转移
  - 舵机轨高功率（7V）和高电流就绪
  - 所有外设输出过流保护，所有输入ESD保护

- 重量和尺寸：
  - 重量：38g（1.31oz）
  - 宽度：50mm（1.96"）
  - 厚度：15.5mm（.613"）
  - 长度：81.5mm（3.21"）

## 可用性

- [裸板](https://store.mrobotics.io/Genuine-PixHawk-1-Barebones-p/mro-pixhawk1-bb-mr.htm) - 仅板子（用作3DR Pixhawk替代品很有用）
- [mRo Pixhawk 2.4.6基本套件！](https://store.mrobotics.io/Genuine-PixHawk-Flight-Controller-p/mro-pixhawk1-minkit-mr.htm) - 除遥测无线电外的所有东西
- [mRo Pixhawk 2.4.6酷套件！（限量版）](https://store.mrobotics.io/product-p/mro-pixhawk1-fullkit-mr.htm) - 您需要的所有东西，包括遥测无线电

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，会由_QGroundControl_自动安装。
:::

要为此目标[构建PX4](../dev_setup/building_px4.md)：

```
make px4_fmu-v3_default
```

## 调试端口

请参见[3DR Pixhawk 1 > 调试端口](../flight_controller/pixhawk.md#debug-ports)

## 引脚图

请参见[3DR Pixhawk 1 > 引脚图](../flight_controller/pixhawk.md#pinouts)

## 串口映射

| UART   | 设备       | 端口                  |
| ------ | ---------- | --------------------- |
| UART1  | /dev/ttyS0 | IO调试                |
| USART2 | /dev/ttyS1 | TELEM1（流控制）      |
| USART3 | /dev/ttyS2 | TELEM2（流控制）      |
| UART4  |            |
| UART7  | CONSOLE    |
| UART8  | SERIAL4    |

<!-- Note: Got ports using https://github.com/PX4/PX4-user_guide/pull/672#issuecomment-598198434 -->

## 原理图

该板基于[Pixhawk项目](https://pixhawk.org/) **FMUv3**开源硬件设计。

- [FMUv3原理图](https://github.com/pixhawk/Hardware/raw/master/FMUv3_REV_D/Schematic%20Print/Schematic%20Prints.PDF) -- 原理图和布局

::: info
作为CC-BY-SA 3.0许可的开源硬件设计，所有原理图和设计文件都[可获得](https://github.com/pixhawk/Hardware)。
:::
