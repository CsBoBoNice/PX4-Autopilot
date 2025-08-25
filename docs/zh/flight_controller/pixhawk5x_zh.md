# Holybro Pixhawk 5X

:::warning
PX4不制造此飞控（或任何其他自动驾驶仪）。
如需硬件支持或合规问题，请联系[制造商](https://holybro.com/)。
:::

_Pixhawk 5X_<sup>&reg;</sup> 是成功的 Pixhawk® 飞控系列的最新更新，由 Holybro<sup>&reg;</sup> 与 PX4 团队协作设计和制造。

它基于 [Pixhawk​​® Autopilot FMUv5X Standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-011%20Pixhawk%20Autopilot%20v5X%20Standard.pdf)、[Autopilot Bus Standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf) 和 [Connector Standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。它预装了最新的 PX4 Autopilot​®，具有三重冗余、温控、隔离传感器域，提供令人难以置信的性能和可靠性。

<img src="../../assets/flight_controller/pixhawk5x/pixhawk5x_hero_upright.jpg" width="250px" title="Pixhawk5x 正面图" /> <img src="../../assets/flight_controller/pixhawk5x/pixhawk5x_exploded_diagram.jpg" width="450px" title="Pixhawk5x 分解图" />

:::tip
此自动驾驶仪得到 PX4 维护和测试团队的[支持](../flight_controller/autopilot_pixhawk_standard.md)。
:::

## 介绍

在 Pixhawk® 5X 内部，您可以找到基于 STMicroelectronics® 的 STM32F7，配对来自 Bosch®、InvenSense® 的传感器技术，为您提供控制任何自主车辆的灵活性和可靠性，适用于学术和商业应用。Pixhawk® 5X 的 F7 微控制器具有 2MB 闪存和 512KB RAM。PX4 Autopilot 利用了增强的功率和 RAM。得益于更新的处理能力，开发人员可以在开发工作中更加高效，允许复杂的算法和模型。

FMUv5X 开放标准包括板载高性能、低噪声 IMU，专为更好的稳定性而设计。三重冗余 IMU 和双重冗余气压计分别在独立总线上。当 PX4 Autopilot 检测到传感器故障时，系统无缝切换到另一个以保持飞行控制可靠性。

独立的 LDO 为每个传感器组供电，具有独立的电源控制。新设计的振动隔离系统，滤除高频振动并减少噪声以确保准确读数，使车辆达到更好的整体飞行性能。外部传感器总线（SPI5）具有两个片选线和数据就绪信号，用于带有 SPI 接口的附加传感器和有效载荷，并且具有集成的 Microchip 以太网 PHY (LAN8742AI-CZ-TR)，现在支持通过以太网与任务计算机进行高速通信。两个智能电池监控端口（SMBus），支持 INA226 SMBus 电源模块。

Pixhawk® 5X 非常适合企业研究实验室、初创公司、学术界（研究、教授、学生）的开发人员以及商业应用。

## 关键设计要点

- 模块化飞控
  - 独立的 IMU、FMU 和基础系统，通过 100 针和 50 针 Pixhawk® Autopilot Bus 连接器连接，专为灵活和可定制的系统而设计
- 冗余
  - 3x IMU 传感器和 2x 气压计传感器分别在独立总线上，即使在硬件故障的情况下也允许并行和连续操作
- 三重冗余域
  - 完全隔离的传感器域，具有独立总线和独立电源控制
- 温控 IMU
  - 板载 IMU 加热电阻器，允许 IMU 的最佳工作温度
- 振动隔离系统
  - 新设计的系统，滤除高频振动并减少噪声以确保准确读数
- 以太网接口
  - 用于高速任务计算机集成
- 自动传感器校准，消除变化的信号和温度
- SMBus 上的两个智能电池监控
- 外部 NFC 读取器的额外 GPIO 线和 5V
- 用于无人机安全认证的安全元件 (SE050)

## 技术规格

- FMU 处理器：STM32F765
  - 32 位 Arm® Cortex®-M7，216MHz，2MB 内存，512KB RAM
- IO 处理器：STM32F100
  - 32 位 Arm® Cortex®-M3，24MHz，8KB SRAM
- 板载传感器：
  - 加速度计/陀螺仪：ICM-20649
  - 加速度计/陀螺仪：ICM-42688P
  - 加速度计/陀螺仪：ICM-20602
  - 磁力计：BMM150
  - 气压计：2x BMP388

- 接口
  - 16 个 PWM 伺服输出
  - Spektrum / DSM 的 R/C 输入
  - PPM 和 S.Bus 输入的专用 R/C 输入
  - 专用模拟 / PWM RSSI 输入和 S.Bus 输出
  - 4 个通用串行端口
    - 3 个具有完整流控制
    - 1 个具有独立 1.5A 电流限制
    - 1 个具有 I2C 和额外 GPIO 线用于外部 NFC 读取器
  - 2 个 GPS 端口
    - 1 个完整的 GPS 和安全开关端口
    - 1 个基本 GPS 端口
  - 1 个 I2C 端口
  - 1 个以太网端口
    - 无变压器应用
  - 100Mbps
  - 1 个 SPI 总线
  - 2 个片选线
  - 2 个数据就绪线
  - 1 个 SPI SYNC 线
  - 1 个 SPI 复位线
  - 2 个 CAN 总线用于 CAN 外设
    - CAN 总线具有独立静音控制或 ESC RX-MUX 控制
  - 2 个具有 SMBus 的电源输入端口
  - 1 个 AD & IO 端口
    - 2 个额外模拟输入
    - 1 个 PWM/捕获输入
    - 2 个专用调试和 GPIO 线

- 电压额定值
  - 最大输入电压：6V
  - USB 电源输入：4.75~5.25V
  - 伺服导轨输入：0~36V

- 尺寸
  - 飞控模块：38.8 x 31.8 x 14.6mm
  - 标准基板：52.4 x 103.4 x 16.7mm

- 重量
  - 飞控模块：23g
  - 标准基板：51g

- 其他特性：
  - 工作和存储温度：-40 ~ 85°c

## 购买地址

从 [Holybro](https://holybro.com/products/pixhawk-5x) 订购。

## 组装/设置

[Pixhawk 5X 接线快速入门](../assembly/quick_start_pixhawk5x.md)提供了如何组装所需/重要外设（包括 GPS、电源模块等）的说明。

## 连接

![Pixhawk 5x 接线概览](../../assets/flight_controller/pixhawk5x/pixhawk5x_wiring_diagram.jpg)

## 引脚定义

![Pixhawk 5X 引脚定义](../../assets/flight_controller/pixhawk5x/pixhawk5x_pinout.png)

::: info
连接器引脚分配从左到右（即引脚 1 是最左侧的引脚）。
:::

注意：

- [相机捕获引脚](../camera/fc_connected_camera.md#camera-capture-configuration)（`PI0`）是 AD&IO 端口上的引脚 2，在上面标记为 `FMU_CAP1`。
- _Pixhawk 5X_ 引脚定义可以从[这里](https://github.com/PX4/PX4-user_guide/blob/main/assets/flight_controller/pixhawk5x/pixhawk5x_pinout.pdf)或[这里](https://cdn.shopify.com/s/files/1/0604/5905/7341/files/Holybro_Pixhawk5X_Pinout.pdf)下载 PDF。

## 串口映射

| UART   | 设备         | 端口            |
| ------ | ---------- | ------------- |
| USART1 | /dev/ttyS0 | GPS           |
| USART2 | /dev/ttyS1 | TELEM3        |
| USART3 | /dev/ttyS2 | 调试控制台         |
| UART4  | /dev/ttyS3 | UART4 & I2C   |
| UART5  | /dev/ttyS4 | TELEM2        |
| USART6 | /dev/ttyS5 | PX4IO/RC      |
| UART7  | /dev/ttyS6 | TELEM1        |
| UART8  | /dev/ttyS7 | GPS2          |

## 尺寸

![Pixhawk 5X 尺寸](../../assets/flight_controller/pixhawk5x/pixhawk5x_dimensions_all.jpg)

## 电压额定值

如果提供三个电源，_Pixhawk 5X_ 可以在电源上实现三重冗余。三个电源轨是：**POWER1**、**POWER2** 和 **USB**。Pixhawk 5X 上的 **POWER1** 和 **POWER2** 端口使用 6 路 [2.00mm 间距 CLIK-Mate 线对板 PCB 插座](https://www.molex.com/en-us/products/part-detail/5024430670)。

**正常操作最大额定值**

在这些条件下，所有电源将按此顺序为系统供电：

1. **POWER1** 和 **POWER2** 输入（4.9V 至 5.5V）
1. **USB** 输入（4.75V 至 5.25V）

**绝对最大额定值**

在这些条件下，系统不会吸取任何电力（不会工作），但将保持完整。

1. **POWER1** 和 **POWER2** 输入（工作范围 4.1V 至 5.7V，0V 至 10V 无损坏）
1. **USB** 输入（工作范围 4.1V 至 5.7V，0V 至 6V 无损坏）
1. 伺服输入：**FMU PWM OUT** 和 **I/O PWM OUT** 的 VDD_SERVO 引脚（0V 至 42V 无损坏）

**电压监控**

默认启用数字 I2C 电池监控（参见[快速入门 > 电源](../assembly/quick_start_pixhawk5x.md#power)）。

::: info
此特定板不支持通过 ADC 进行模拟电池监控，但在具有不同基板的此飞控变体中可能受支持。
:::

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时由 _QGroundControl_ 自动安装。
:::

为此目标[构建 PX4](../dev_setup/building_px4.md)：

```
make px4_fmu-v5x_default
```

<a id="debug_port"></a>

## 调试端口

[PX4 系统控制台](../debug/system_console.md)和 [SWD 接口](../debug/swd_debug.md)在 **FMU Debug** 端口上运行。

引脚定义和连接器符合在 [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)接口中定义的 [Pixhawk Debug Full](../debug/swd_debug.md#pixhawk-debug-full) 接口（JST SM10B 连接器）。

| 引脚       | 信号             | 电压  |
| -------- | -------------- | --- |
| 1（红）    | `Vtref`        | +3.3V |
| 2（黑）    | 控制台 TX（OUT）   | +3.3V |
| 3（黑）    | 控制台 RX（IN）    | +3.3V |
| 4（黑）    | `SWDIO`        | +3.3V |
| 5（黑）    | `SWCLK`        | +3.3V |
| 6（黑）    | `SWO`          | +3.3V |
| 7（黑）    | NFC GPIO       | +3.3V |
| 8（黑）    | PH11           | +3.3V |
| 9（黑）    | nRST           | +3.3V |
| 10（黑）   | `GND`          | GND |

有关使用此端口的信息，请参阅：

- [SWD 调试端口](../debug/swd_debug.md)
- [PX4 系统控制台](../debug/system_console.md)（注意，FMU 控制台映射到 USART3）。

## 外设

- [数字空速传感器](https://holybro.com/products/digital-air-speed-sensor-ms4525do)
- [遥测无线电模块](https://holybro.com/collections/telemetry-radios?orderby=date)
- [测距仪/距离传感器](../sensor/rangefinders.md)

## 支持的平台/机架

任何可以用正常 RC 伺服或 Futaba S-Bus 伺服控制的多旋翼/飞机/漫游车或船只。完整的支持配置集合可以在[机架参考](../airframes/airframe_reference.md)中看到。

## 更多信息

- [Pixhawk 5X 接线快速入门](../assembly/quick_start_pixhawk5x.md)
- [Pixhawk 5X 概述和规格](https://cdn.shopify.com/s/files/1/0604/5905/7341/files/Holybro_Pixhawk5X_Spec_Overview.pdf)（Holybro）
- [Pixhawk 5X 引脚定义](https://cdn.shopify.com/s/files/1/0604/5905/7341/files/Holybro_Pixhawk5X_Pinout.pdf)（Holybro）
- [FMUv5X 参考设计引脚定义](https://docs.google.com/spreadsheets/d/1Su7u8PHp-Y1AlLGVuH_I8ewkEEXt_bHHYBHglRuVH7E/edit#gid=562580340)。
- [Pixhawk Autopilot FMUv5X 标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-011%20Pixhawk%20Autopilot%20v5X%20Standard.pdf)。
- [Pixhawk Autopilot Bus 标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf)。
- [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。
