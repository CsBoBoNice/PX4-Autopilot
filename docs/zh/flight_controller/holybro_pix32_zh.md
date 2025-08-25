# Holybro pix32 飞行控制器（已停产）

<Badge type="info" text="已停产" />

:::warning
PX4 不生产此（或任何）自驾仪。
如有硬件支持或合规性问题，请联系[制造商](https://holybro.com/)。
:::

Holybro<sup>&reg;</sup> [pix32 自驾仪](https://holybro.com/products/pix32pixhawk-flight-controller)（也被称为"Pixhawk 2"，以前称为 HKPilot32）基于 [Pixhawk<sup>&reg;</sup> 项目](https://pixhawk.org/) **FMUv2** 开源硬件设计。
此板基于硬件版本 Pixhawk 2.4.6。
它在 [NuttX](https://nuttx.apache.org/) 操作系统上运行 PX4 飞行栈。

![pix32](../../assets/flight_controller/holybro_pix32/pix32_hero.jpg)

作为 CC-BY-SA 3.0 许可的开源硬件设计，原理图和设计文件应[在此处可用](https://github.com/pixhawk/Hardware)。

:::tip
Holybro pix32 在软件上与 [3DR Pixhawk 1](../flight_controller/pixhawk.md) 兼容。
它在连接器上不兼容，但在物理上与 3DR Pixhawk 或 mRo Pixhawk 非常相似。
:::

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 主要特点

- 主系统芯片：[STM32F427](https://www.st.com/en/microcontrollers-microprocessors/stm32f427-437.html)
  - CPU：32位 STM32F427 Cortex<sup>&reg;</sup> M4 核心带 FPU
  - RAM：168 MHz/256 KB
  - Flash：2 MB
- 故障安全系统芯片：STM32F103
- 传感器：
  - ST Micro L3GD20 3轴 16位陀螺仪
  - ST Micro LSM303D 3轴 14位加速度计/磁力计
  - Invensense<sup>&reg;</sup> MPU 6000 3轴加速度计/陀螺仪
  - MEAS MS5611 气压计
- 尺寸/重量
  - 尺寸：81x44x15mm
  - 重量：33.1g
- GPS：u-blox<sup>&reg;</sup> 超精密 Neo-7M 带指南针
- 输入电压：2~10s（7.4~37V）

### 连接性

- 1x I2C
- 2x CAN
- 3.3 和 6.6V ADC 输入
- 5x UART（串行端口），1个高功率兼容，2x 带硬件流量控制
- Spektrum DSM / DSM2 / DSM-X® 卫星兼容输入，最高支持 DX8（不支持 DX9 及以上）
- Futaba<sup>&reg;</sup> S.BUS 兼容输入和输出
- PPM 和信号
- RSSI（PWM 或电压）输入
- SPI
- 外部 microUSB 端口
- Molex PicoBlade 连接器

## 购买地点

[shop.holybro.com](https://holybro.com/products/pix32pixhawk-flight-controller)

### 配件

- [数字空速传感器](https://holybro.com/products/digital-air-speed-sensor-ms4525do)
- [HolyBro SiK 遥测无线电（欧盟 433 MHz，美国 915 MHz）](../telemetry/holybro_sik_radio.md)

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，_QGroundControl_ 会自动安装。
:::

要为此目标[构建 PX4](../dev_setup/building_px4.md)：

```
make px4_fmu-v2_default
```

## 调试端口

请参阅 [3DR Pixhawk 1 > 调试端口](../flight_controller/pixhawk.md#debug-ports)。

## 引脚分布和原理图

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
