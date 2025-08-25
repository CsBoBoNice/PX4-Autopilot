# AUAV-X2 自驾仪（已停产）

<Badge type="info" text="已停产" />

:::warning
此飞行控制器已[停产](../flight_controller/autopilot_experimental.md)，不再商业化销售。
:::

:::warning
PX4 不生产此（或任何）自驾仪。
如有硬件支持或合规性问题，请联系[制造商](https://store.mrobotics.io/)。
:::

AUAV-X2 自驾仪基于 [Pixhawk<sup>&reg;</sup> 项目](https://pixhawk.org/) **FMUv2** 开源硬件设计。它在 [NuttX](https://nuttx.apache.org/) 操作系统上运行 PX4。

![AUAVX2_case2](../../assets/flight_controller/auav_x2/auavx2_case2.jpg)

## 快速总结

- 主系统芯片：[STM32F427](https://www.st.com/en/microcontrollers-microprocessors/stm32f427-437.html)
  - CPU：STM32F427VIT6 ARM 微控制器 - 第3版
  - IO：STM32F100C8T6 ARM 微控制器
- 传感器：
  - Invensense MPU9250 9DOF
  - Invensense ICM-20608 6DOF
  - MEAS MS5611 气压计
- 尺寸/重量
  - 尺寸：36mm x 50mm
  - 安装点：30.5mm x 30.5mm 3.2mm 直径
  - 重量：10.9g
- 带反向电压保护的电源或门原理图。需要 5V 电源模块！

## 连接性

- 2.54mm 排针：
- GPS（USART4）
- i2c
- RC 输入
- PPM 输入
- Spektrum 输入
- RSSI 输入
- sBus 输入
- sBus 输出
- 电源输入
- 蜂鸣器输出
- LED 输出
- 8 x 舵机输出
- 6 x 辅助输出
- USART7（控制台）
- USART8（OSD）

## 可用性

不再生产。
已被 [mRo X2.1](mro_x2.1.md) 取代。
从 2017 年 8 月起，mRobotics 是 AUAV 产品的分销商。

## 关键链接

- [用户手册](http://arsovtech.com/wp-content/uploads/2015/08/AUAV-X2-user-manual-EN.pdf)
- [DIY Drones 帖子](https://diydrones.com/profiles/blogs/introducing-the-auav-x2-1-flight-controller)

## 接线指南

![AUAV-X2-basic-setup 3](../../assets/flight_controller/auav_x2/auav_x2_basic_setup_3.png)

![AUAV-X2-basic-setup 2](../../assets/flight_controller/auav_x2/auav_x2_basic_setup_2.jpg)

![AUAV-X2-basic-setup 1](../../assets/flight_controller/auav_x2/auav_x2_basic_setup_1.png)

![AUAV-X2-airspeed-setup 3](../../assets/flight_controller/auav_x2/auav_x2_airspeed_setup_3.png)

## 原理图

该板基于 [Pixhawk 项目](https://pixhawk.org/) **FMUv2** 开源硬件设计。

- [FMUv2 + IOv2 原理图](https://raw.githubusercontent.com/PX4/Hardware/master/FMUv2/PX4FMUv2.4.5.pdf) -- 原理图和布局

::: info
作为 CC-BY-SA 3.0 许可的开源硬件设计，所有原理图和设计文件都[可获得](https://github.com/pixhawk/Hardware)。
:::

## 串行端口映射

| UART   | 设备       | 端口                  |
| ------ | ---------- | --------------------- |
| UART1  | /dev/ttyS0 | IO 调试               |
| USART2 | /dev/ttyS1 | TELEM1（流量控制）    |
| USART3 | /dev/ttyS2 | TELEM2（流量控制）    |
| UART4  |            |
| UART7  | CONSOLE    |
| UART8  | SERIAL4    |
