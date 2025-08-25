# 3DR Pixhawk 1 飞控（已停产）

:::warning
此飞控已[停产](../flight_controller/autopilot_experimental.md)，不再有商业销售。
您可以使用 [mRo Pixhawk](../flight_controller/mro_pixhawk.md) 作为直接替代品。
:::

:::warning
PX4不制造此飞控（或任何其他自动驾驶仪）。
如需支持或合规问题，请联系制造商。
:::

_3DR Pixhawk<sup>&reg;</sup> 1_ 自动驾驶仪是一种流行的通用飞控，基于 [Pixhawk-project](https://pixhawk.org/) **FMUv2** 开放硬件设计（它结合了 PX4FMU + PX4IO 的功能）。它在 [NuttX](https://nuttx.apache.org/) OS 上运行 PX4。

![Pixhawk 图片](../../assets/hardware/hardware-pixhawk.png)

PX4使用说明的组装/设置说明在此处提供：[Pixhawk 接线快速入门](../assembly/quick_start_pixhawk.md)

## 主要特性

- 主系统级芯片：[STM32F427](https://www.st.com/en/microcontrollers-microprocessors/stm32f427-437.html)
  - CPU：180 MHz ARM<sup>&reg;</sup> Cortex<sup>&reg;</sup> M4 单精度 FPU
  - RAM：256 KB SRAM (L1)
- 故障安全系统级芯片：STM32F100
  - CPU：24 MHz ARM Cortex M3
  - RAM：8 KB SRAM
- Wifi：ESP8266 外置
- GPS：u-blox<sup>&reg;</sup> 7/8 (Hobbyking<sup>&reg;</sup>) / u-blox 6 (3D Robotics)
- 光流：[PX4 Flow 单元](../sensor/px4flow.md)
- 冗余电源输入和自动故障转移
- 外部安全开关
- 多色 LED 主视觉指示器
- 高功率多音调压电音频指示器
- microSD 卡用于长时间高速率记录

连接性

- 1x I2C
- 1x CAN（2x 可选）
- 1x ADC
- 4x UART（2x 具有流控制）
- 1x 控制台
- 8x PWM 具有手动覆盖
- 6x PWM / GPIO / PWM 输入
- S.BUS / PPM / Spektrum 输入
- S.BUS 输出

# 购买地址

最初由 3DR&reg; 制造，该板是 PX4&reg; 的原始标准微控制器平台。虽然该板不再由 3DR 制造，但您可以使用 [mRo Pixhawk](../flight_controller/mro_pixhawk.md) 作为直接替代品。

从以下地址订购 mRo Pixhawk：

- [Bare Bones](https://store.mrobotics.io/Genuine-PixHawk-1-Barebones-p/mro-pixhawk1-bb-mr.htm) - 仅主板（作为 3DR Pixhawk 替代品很有用）
- [mRo Pixhawk 2.4.6 Essential Kit](https://store.mrobotics.io/Genuine-PixHawk-Flight-Controller-p/mro-pixhawk1-minkit-mr.htm) - 除遥测无线电外包含所有内容
- [mRo Pixhawk 2.4.6 Cool Kit!（限量版）](https://store.mrobotics.io/product-p/mro-pixhawk1-fullkit-mr.htm) - 包含您需要的一切，包括遥测无线电

## 规格

### 处理器

- 32位 STM32F427 [Cortex-M4F](https://en.wikipedia.org/wiki/ARM_Cortex-M#Cortex-M4) 核心，具有 FPU
- 168 MHz
- 256 KB RAM
- 2 MB Flash
- 32 位 STM32F103 故障安全协处理器

### 传感器

- ST Micro L3GD20H 16 位陀螺仪
- ST Micro LSM303D 14 位加速度计/磁力计
- Invensense MPU 6000 3轴加速度计/陀螺仪
- MEAS MS5611 气压计

### 接口

- 5x UART（串行端口），一个高功率能力，2x 具有硬件流控制
- 2x CAN（一个具有内部 3.3V 收发器，一个在扩展连接器上）
- Spektrum DSM / DSM2 / DSM-X® 卫星兼容输入
- Futaba S.BUS® 兼容输入和输出
- PPM 总和信号输入
- RSSI（PWM 或电压）输入
- I2C
- SPI
- 3.3 和 6.6V ADC 输入
- 内部 microUSB 端口和外部 microUSB 端口扩展

<lite-youtube videoid="gCCC5A-Bvv4" title="PX4 Pixhawk (3DR) Multicolor Led in action"/>

### 电源系统和保护

- 具有自动故障转移的理想二极管控制器
- 伺服导轨高功率（最大 10V）和高电流（10A+）就绪
- 所有外设输出过流保护，所有输入 ESD 保护

## 电压额定值

如果提供三个电源，Pixhawk 可以在电源上实现三重冗余。三个电源轨是：电源模块输入、伺服导轨输入、USB 输入。

### 正常操作最大额定值

在这些条件下，所有电源将按此顺序为系统供电

- 电源模块输入（4.8V 至 5.4V）
- 伺服导轨输入（4.8V 至 5.4V）**最高 10V 用于手动覆盖，但如果电源模块输入不存在，自动驾驶仪部分在 5.7V 以上将断电**
- USB 电源输入（4.8V 至 5.4V）

### 绝对最大额定值

在这些条件下，系统不会吸取任何电力（不会工作），但将保持完整。

- 电源模块输入（4.1V 至 5.7V，0V 至 20V 无损坏）
- 伺服导轨输入（4.1V 至 5.7V，0V 至 20V）
- USB 电源输入（4.1V 至 5.7V，0V 至 6V）

## 原理图

[FMUv2 + IOv2 原理图](https://raw.githubusercontent.com/PX4/Hardware/master/FMUv2/PX4FMUv2.4.5.pdf) -- 原理图和布局

::: info
作为 CC-BY-SA 3.0 许可的开放硬件设计，所有原理图和设计文件都[可用](https://github.com/pixhawk/Hardware)。
:::

## 连接

Pixhawk 端口如下所示。这些使用 Hirose DF13 连接器（早于 Pixhawk 连接器标准中定义的 JST-GH 连接器）。

:::warning
许多 3DR Pixhawk 克隆使用 Molex picoblade 连接器而不是 DF13 连接器。它们有矩形而不是方形引脚，不能假定兼容。
:::

![Pixhawk 连接器](../../assets/flight_controller/pixhawk1/pixhawk_connectors.png)

:::tip
`RC IN` 端口仅用于 RC 接收器，并为此目的提供足够的电源。**绝不要**将任何伺服、电源或电池连接到它或连接到它的接收器。
:::

## 引脚定义

#### TELEM1、TELEM2 端口

| 引脚      | 信号      | 电压  |
| ------- | ------- | --- |
| 1（红）   | VCC     | +5V |
| 2（黑）   | TX（OUT） | +3.3V |
| 3（黑）   | RX（IN）  | +3.3V |
| 4（黑）   | CTS（IN） | +3.3V |
| 5（黑）   | RTS（OUT） | +3.3V |
| 6（黑）   | GND     | GND |

#### GPS 端口

| 引脚      | 信号       | 电压  |
| ------- | -------- | --- |
| 1（红）   | VCC      | +5V |
| 2（黑）   | TX（OUT） | +3.3V |
| 3（黑）   | RX（IN）  | +3.3V |
| 4（黑）   | CAN2 TX  | +3.3V |
| 5（黑）   | CAN2 RX  | +3.3V |
| 6（黑）   | GND      | GND |

#### SERIAL 4/5 端口

由于空间限制，两个端口在一个连接器上。

| 引脚      | 信号      | 电压  |
| ------- | ------- | --- |
| 1（红）   | VCC     | +5V |
| 2（黑）   | TX（#4） | +3.3V |
| 3（黑）   | RX（#4） | +3.3V |
| 4（黑）   | TX（#5） | +3.3V |
| 5（黑）   | RX（#5） | +3.3V |
| 6（黑）   | GND     | GND |

#### ADC 6.6V

| 引脚      | 信号     | 电压         |
| ------- | ------ | ---------- |
| 1（红）   | VCC    | +5V        |
| 2（黑）   | ADC IN | 最高 +6.6V |
| 3（黑）   | GND    | GND        |

#### ADC 3.3V

| 引脚      | 信号     | 电压         |
| ------- | ------ | ---------- |
| 1（红）   | VCC    | +5V        |
| 2（黑）   | ADC IN | 最高 +3.3V |
| 3（黑）   | GND    | GND        |
| 4（黑）   | ADC IN | 最高 +3.3V |
| 5（黑）   | GND    | GND        |

#### I2C

| 引脚      | 信号  | 电压            |
| ------- | --- | ------------- |
| 1（红）   | VCC | +5V           |
| 2（黑）   | SCL | +3.3（上拉）     |
| 3（黑）   | SDA | +3.3（上拉）     |
| 4（黑）   | GND | GND           |

#### CAN

| 引脚      | 信号     | 电压   |
| ------- | ------ | ---- |
| 1（红）   | VCC    | +5V  |
| 2（黑）   | CAN_H  | +12V |
| 3（黑）   | CAN_L  | +12V |
| 4（黑）   | GND    | GND  |

#### SPI

| 引脚      | 信号            | 电压  |
| ------- | ------------- | --- |
| 1（红）   | VCC           | +5V |
| 2（黑）   | SPI_EXT_SCK   | +3.3 |
| 3（黑）   | SPI_EXT_MISO  | +3.3 |
| 4（黑）   | SPI_EXT_MOSI  | +3.3 |
| 5（黑）   | !SPI_EXT_NSS  | +3.3 |
| 6（黑）   | !GPIO_EXT     | +3.3 |
| 7（黑）   | GND           | GND |

#### POWER

| 引脚      | 信号      | 电压  |
| ------- | ------- | --- |
| 1（红）   | VCC     | +5V |
| 2（黑）   | VCC     | +5V |
| 3（黑）   | CURRENT | +3.3V |
| 4（黑）   | VOLTAGE | +3.3V |
| 5（黑）   | GND     | GND |
| 6（黑）   | GND     | GND |

#### SWITCH

| 引脚      | 信号             | 电压  |
| ------- | -------------- | --- |
| 1（红）   | VCC            | +3.3V |
| 2（黑）   | !IO_LED_SAFETY | GND |
| 3（黑）   | SAFETY         | GND |

## 串口映射

| UART   | 设备         | 端口                    |
| ------ | ---------- | --------------------- |
| UART1  | /dev/ttyS0 | IO 调试                 |
| USART2 | /dev/ttyS1 | TELEM1（流控制）          |
| USART3 | /dev/ttyS2 | TELEM2（流控制）          |
| UART4  |            |                       |
| UART7  | 控制台        |                       |
| UART8  | SERIAL4    |                       |

<!-- Note: Got ports using https://github.com/PX4/PX4-user_guide/pull/672#issuecomment-598198434 -->

## 调试端口

### 控制台端口

[PX4 系统控制台](../debug/system_console.md)在标记为 [SERIAL4/5](#serial-4-5-port) 的端口上运行。

:::tip
连接到控制台的便捷方法是使用 [Zubax BugFace BF1](https://github.com/Zubax/bugface_bf1)，因为它带有可与多个不同 Pixhawk 设备一起使用的连接器。只需将 [Zubax BugFace BF1](https://github.com/Zubax/bugface_bf1) 上的 6 位 DF13 1:1 电缆连接到 Pixhawk `SERIAL4/5` 端口。

![Zubax BugFace BF1](../../assets/flight_controller/pixhawk1/dronecode_probe.jpg)
:::

引脚定义是标准串行引脚定义，设计用于连接 [3.3V FTDI](https://www.digikey.com/en/products/detail/TTL-232R-3V3/768-1015-ND/1836393) 电缆（5V 容许）。

| 3DR Pixhawk 1 |            | FTDI |              |
| ------------- | ---------- | ---- | ------------ |
| 1             | +5V（红）    |      | N/C          |
| 2             | S4 Tx      |      | N/C          |
| 3             | S4 Rx      |      | N/C          |
| 4             | S5 Tx      | 5    | FTDI RX（黄） |
| 5             | S5 Rx      | 4    | FTDI TX（橙） |
| 6             | GND        | 1    | FTDI GND（黑） |

FTDI 电缆到 6 位 DF13 1:1 连接器的接线如下图所示。

![控制台连接器](../../assets/flight_controller/pixhawk1/console_connector.jpg)

完整接线如下所示。

![控制台调试](../../assets/flight_controller/pixhawk1/console_debug.jpg)

::: info
有关如何_使用_控制台的信息，请参阅：[系统控制台](../debug/system_console.md)。
:::

### SWD 端口

[SWD](../debug/swd_debug.md)（JTAG）端口隐藏在盖子下面（必须拆除以进行硬件调试）。FMU 和 IO 有单独的端口，如下所示。

![Pixhawk SWD](../../assets/flight_controller/pixhawk1/pixhawk_swd.jpg)

端口是 ARM 10 针 JTAG 连接器，您可能需要焊接。端口的引脚定义如下所示（上面拐角的方形标记表示引脚 1）。

![ARM 10针连接器引脚定义](../../assets/flight_controller/pixhawk1/arm_10pin_jtag_connector_pinout.jpg)

::: info
所有 Pixhawk FMUv2 板都有类似的 SWD 端口。
:::

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时由 _QGroundControl_ 自动安装。
:::

为此目标[构建 PX4](../dev_setup/building_px4.md)：

```
make px4_fmu-v2_default
```

## 零件/外壳

- **ARM MINI JTAG (J6)**：1.27 mm 10 位头（SHROUDED），用于 Black Magic Probe：FCI 20021521-00010D4LF ([Digi-Key](https://www.digikey.com/en/products/detail/20021521-00010T1LF/609-4054-ND/2414951),) 或 Samtec FTSH-105-01-F-DV-K (未测试) 或 Harwin M50-3600542 ([Digikey](https://www.digikey.com/en/products/detail/harwin-inc/M50-3600542/2264370))
  - JTAG 适配器选项 #1：[BlackMagic Probe](https://1bitsquared.com/products/black-magic-probe)。注意，可能没有电缆（请与制造商确认）。如果是这样，您将需要 **Samtec FFSD-05-D-06.00-01-N** 电缆 ([Samtec 样品服务](https://www.samtec.com/products/ffsd-05-d-06.00-01-n) 或 [Digi-Key Link: SAM8218-ND](https://www.digikey.com/en/products/detail/samtec-inc/ffsd-05-d-06-00-01-n/1106577)) 或 [Tag Connect Ribbon](https://www.tag-connect.com/product/10-pin-cortex-ribbon-cable-4-length-with-50-mil-connectors) 和 Mini-USB 电缆。
  - JTAG 适配器选项 #2：[Digi-Key Link: ST-LINK/V2](https://www.digikey.com/product-detail/en/stmicroelectronics/ST-LINK-V2/497-10484-ND) / [ST USER MANUAL](https://www.st.com/resource/en/user_manual/dm00026748.pdf)，需要 ARM Mini JTAG 到 20 位适配器：[Digi-Key Link: 726-1193-ND](https://www.digikey.com/en/products/detail/texas-instruments/MDL-ADA2/1986451)
  - JTAG 适配器选项 #3：[Olimex ARM-TINY](https://www.olimex.com/wiki/ARM-USB-TINY) 或任何其他 OpenOCD 兼容的 ARM Cortex JTAG 适配器，需要 ARM Mini JTAG 到 20 位适配器：[Digi-Key Link: 726-1193-ND](https://www.digikey.com/en/products/detail/texas-instruments/MDL-ADA2/1986451)
- **USARTs**：Hirose DF13 6 位 ([Digi-Key Link: DF13A-6P-1.25H(20)](https://www.digikey.com/products/en?keywords=H3371-ND))
  - 配对：Hirose DF13 6 位外壳 ([Digi-Key Link: Hirose DF13-6S-1.25C](https://www.digikey.com/products/en?keywords=H2182-ND))
- **I2C 和 CAN**：Hirose DF13 4 位 ([Digi-Key Link: DF13A-4P-1.25H(20)](https://www.digikey.com/en/products/detail/hirose-electric-co-ltd/DF13A-4P-1-25H-20/530666) - 已停产)

## 支持的平台/机架

任何可以用正常 RC 伺服或 Futaba S-Bus 伺服控制的多旋翼/飞机/漫游车或船只。
