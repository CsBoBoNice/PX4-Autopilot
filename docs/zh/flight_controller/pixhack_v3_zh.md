# CUAV Pixhack V3（已停产）

<Badge type="info" text="已停产" />

:::warning
此飞行控制器已[停产](../flight_controller/autopilot_experimental.md)，不再有商业销售。
:::

:::warning
PX4 不制造这个（或任何）自动驾驶仪。
请联系[制造商](https://store.cuav.net/)获取硬件支持或合规问题。
:::

CUAV _Pixhack V3_飞行控制器板是一个灵活的自动驾驶仪，主要面向商业系统制造商。

该板是SOLO Pixhawk<sup>&reg;</sup> 2（PH2）飞行控制器的变体，而PH2基于[Pixhawk项目](https://pixhawk.org/) **FMUv3**开源硬件设计。
它在[NuttX](https://nuttx.apache.org/) OS上运行PX4，并且与PX4或ArduPilot<sup>&reg;</sup>（APM）固件完全兼容。

相对于原始设计，_Pixhack V3_有显著改进，包括更好的接口布局以及增加了振动阻尼和恒温系统。

![Pixhack v3](../../assets/flight_controller/pixhack_v3/pixhack_v3_157_large_default.jpg)

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 快速摘要

- 微处理器：
  - STM32F427
  - STM32F100（故障安全协处理器）
- 传感器：
  - 加速度计（3个）：LS303D、MPU6000、MPU9250/hmc5983
  - 陀螺仪（3个）：L3GD20、MPU6000、MPU9250
  - 指南针（2个）：LS303D、MPU9250
  - 气压计（2个）：MS5611 X2
- 接口：
  - MAVLink UART（2个）
  - GPS UART（2个）
  - DEBUG UART（1个）
  - RC IN（用于PPM、SBUS、DSM/DSM2）
  - RSSI IN：PWM或3.3ADC
  - I2C（2个）
  - CAN BUS（1个）
  - ADC IN：3.3V X1，6.6V X1
  - PWM OUT：8个PWM IO + 4个IO
- 电源系统：
  - PM POWER IN：4.5 ~ 5.5 V
  - USB POWER IN：5.0 V +- 0.25v
- 重量和尺寸：
  - 重量：63g
  - 宽度：68mm
  - 厚度：17mm
  - 长度：44mm
- 其他特性：
  - 工作温度：-20 ~ 60°C

## 可用性

该板可从以下地方购买：

- [leixun.aliexpress.com/store](https://leixun.aliexpress.com/store)

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，会由_QGroundControl_自动安装。
:::

要为此目标[构建PX4](../dev_setup/building_px4.md)：

```sh
make px4_fmu-v3_default
```

<!-- Pinouts and Schematics: section removed as guides no longer published -->

## 串口映射

| UART   | 设备       | 端口                  |
| ------ | ---------- | --------------------- |
| UART1  | /dev/ttyS0 | IO调试                |
| USART2 | /dev/ttyS1 | TELEM1（流控制）      |
| USART3 | /dev/ttyS2 | TELEM2（流控制）      |
| UART4  |            |                       |
| UART7  |            | 控制台                |
| UART8  |            | SERIAL4               |
