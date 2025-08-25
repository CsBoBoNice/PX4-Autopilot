# Holybro Pix32 v5

:::warning
PX4 不生产此（或任何）自驾仪。
如有硬件支持或合规性问题，请联系[制造商](https://holybro.com/)。
:::

[Pix32 v5](https://holybro.com/products/pix32-v5)<sup>&reg;</sup> 是由 Holybro<sup>&reg;</sup> 设计和制造的先进自驾仪飞行控制器。
它针对运行 PX4 固件进行了优化，面向学术和商业开发者。
它基于 [Pixhawk 项目](https://pixhawk.org/) **FMUv5** 开源硬件设计，在 [NuttX](https://nuttx.apache.org/) 操作系统上运行 PX4。
它可以看作是 Pixhawk4 的变体版本。

Pix32 v5 专为需要高功率、灵活且可定制飞行控制系统的飞行员设计。
它由独立的飞行控制器和载板（基板）组成，通过 100 针连接器连接。
这种设计允许用户选择 Holybro 制造的基板，或定制自己的基板。

![Pix32 v5 Family](../../assets/flight_controller/holybro_pix32_v5/pix32_v5_family.jpg)

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

## 快速总结

- 主 FMU 处理器：STM32F765
  - 32 位 Arm® Cortex®-M7，216MHz，2MB 内存，512KB RAM
- IO 处理器：STM32F100
  - 32 位 Arm® Cortex®-M3，24MHz，8KB SRAM
- 板载传感器：
  - 加速度计/陀螺仪：ICM-20689
  - 加速度计/陀螺仪：BMI055 或 ICM20602
  - 磁力计：IST8310
  - 气压计：MS5611
- GPS：u-blox Neo-M8N GPS/GLONASS 接收器；集成磁力计 IST8310
- 接口：
  - 8-16 个 PWM 输出（8 个来自 IO，8 个来自 FMU）
  - FMU 上 3 个专用 PWM/捕获输入
  - CPPM 专用 R/C 输入
  - Spektrum / DSM 和 S.Bus 专用 R/C 输入，带模拟/PWM RSSI 输入
  - 专用 S.Bus 舵机输出
  - 5 个通用串行端口
    - 2 个带完整流量控制
    - 1 个带独立 1.5A 电流限制
  - 3 个 I2C 端口
  - 4 个 SPI 总线
    - 1 个内部高速 SPI 传感器总线，带 4 个片选和 6 个 DRDY
    - 1 个内部低噪音 SPI 总线专用于
    - 气压计，带 2 个片选，无 DRDY
    - 1 个内部 SPI 总线专用于 FRAM
    - 支持位于传感器模块上的专用 SPI 校准 EEPROM
    - 1 个外部 SPI 总线
  - 最多 2 个 CAN 总线，用于双 CAN 与串行 ESC
    - 每个 CAN 总线都有独立的静默控制或 ESC RX-MUX 控制
    - 2 个电池的电压/电流模拟输入
    - 2 个额外的模拟输入
- 电气系统：
  - 电源模块输出：4.9~5.5V
  - 最大输入电压：6V
  - 最大电流检测：120A
  - USB 电源输入：4.75~5.25V
  - 舵机导轨输入：0~36V
- 重量和尺寸：
  - 尺寸：45x45x13.5mm
  - 重量：33.0g
- 环境数据、质量和可靠性：
  - 工作温度：-40 ~ 85°c
  - 存储温度：-40~85℃
  - CE
  - FCC
  - RoHS 合规（无铅）

更多信息可在 [Pix32 V5 技术数据表](https://cdn.shopify.com/s/files/1/0604/5905/7341/files/Holybro_PIX32-V5_technical_data_sheet_v1.1.pdf) 中找到。

## 购买地点

从 [Holybro 网站](https://holybro.com/products/pix32-v5) 订购。

## 组装/设置

[Pix32 v5 接线快速入门](../assembly/quick_start_holybro_pix32_v5.md) 提供了如何组装必需/重要外设（包括 GPS、电源管理板等）的说明。

## 基板布局

![Pix32 v5 Image](../../assets/flight_controller/holybro_pix32_v5/pix32_v5_base_boards_layout.jpg)

## 引脚分布

[_pix32 v5_ 和 mini 基板](https://cdn.shopify.com/s/files/1/0604/5905/7341/files/Holybro_Pix32-V5-Base-Mini-Pinouts.pdf)

## 尺寸

![Pix32 v5 Image](../../assets/flight_controller/holybro_pix32_v5/Dimensions_no_border.jpg)

## 电压额定值

如果提供三个电源，_Pix32 v5_ 可在电源上实现三重冗余。
三个电源导轨是：**POWER1**、**POWER2** 和 **USB**。

::: info
输出电源导轨 **FMU PWM OUT** 和 **I/O PWM OUT**（0V 至 36V）不为飞行控制器板供电（也不由其供电）。
您必须向 **POWER1**、**POWER2** 或 **USB** 之一供电，否则板卡将无电源。
:::

**正常操作最大额定值**

在这些条件下，所有电源将按此顺序用于为系统供电：

1. **POWER1** 和 **POWER2** 输入（4.9V 至 5.5V）
1. **USB** 输入（4.75V 至 5.25V）

**绝对最大额定值**

在这些条件下，系统将不会汲取任何电力（不会运行），但将保持完整。

1. **POWER1** 和 **POWER2** 输入（工作范围 4.1V 至 5.7V，0V 至 10V 不损坏）
1. **USB** 输入（工作范围 4.1V 至 5.7V，0V 至 6V 不损坏）
1. 舵机输入：**FMU PWM OUT** 和 **I/O PWM OUT** 的 VDD_SERVO 引脚（0V 至 42V 不损坏）

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，_QGroundControl_ 会自动安装。
:::

要为此目标[构建 PX4](../dev_setup/building_px4.md)：

```
make holybro_pix32v5_default
```

## 调试端口

系统的[串行控制台](../debug/system_console.md)和 SWD 接口在 **FMU 调试** 端口上运行

<!--while the I/O console and SWD interface can be accessed via **I/O Debug** port.-->

![FMU debug port diagram](../../assets/flight_controller/holybro_pix32_v5/FMU_Debug_Port_Horizontal.jpg)

引脚分布使用在 [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf) 中定义的标准 [Pixhawk Debug Mini](../debug/swd_debug.md#pixhawk-debug-mini) 接口。

## 外设

- [数字空速传感器](../sensor/airspeed.md)
- [遥测无线电模块](../telemetry/index.md)
- [测距仪/距离传感器](../sensor/rangefinders.md)

## 支持的平台/机架

任何可以用普通 RC 舵机或 Futaba S-Bus 舵机控制的多旋翼/固定翼/地面车辆或船只。
完整的支持配置可以在[机架参考](../airframes/airframe_reference.md)中看到。

## 附加信息

- [Pix32 v5 技术数据表](https://cdn.shopify.com/s/files/1/0604/5905/7341/files/Holybro_PIX32-V5_technical_data_sheet_v1.1.pdf)
- [Pix32 v5 引脚分布](https://cdn.shopify.com/s/files/1/0604/5905/7341/files/Holybro_Pix32-V5-Base-Mini-Pinouts.pdf)
- [Pix32 v5 基板原理图](https://cdn.shopify.com/s/files/1/0604/5905/7341/files/Holybro_PIX32-V5-BASE-Schematic_diagram.pdf)
- [Pix32 v5 Mini 基板原理图](https://cdn.shopify.com/s/files/1/0604/5905/7341/files/Holybro_PIX32-V5-Base-Mini-Board_Schematic_diagram.pdf)
- [FMUv5 参考设计引脚分布](https://docs.google.com/spreadsheets/d/1-n0__BYDedQrc_2NHqBenG1DNepAgnHpSGglke-QQwY/edit#gid=912976165)