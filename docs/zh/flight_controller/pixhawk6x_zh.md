# Holybro Pixhawk 6X

:::warning
PX4不制造此飞控（或任何其他自动驾驶仪）。
如需硬件支持或合规问题，请联系[制造商](https://holybro.com/)。
:::

_Pixhawk 6X_<sup>&reg;</sup> 是成功的 Pixhawk® 飞控系列的最新更新，由 Holybro<sup>&reg;</sup> 与 PX4 团队协作设计和制造。

它基于 [Pixhawk​​® Autopilot FMUv6X Standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-012%20Pixhawk%20Autopilot%20v6X%20Standard.pdf)、[Autopilot Bus Standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf) 和 [Connector Standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。

配备高性能 H7 处理器、模块化设计、三重冗余、温控 IMU 板和隔离传感器域，提供令人难以置信的性能、可靠性和灵活性。

### Pixhawk 6X (Rev 8)

<img src="../../assets/flight_controller/pixhawk6x/HB_6X_rev8_V2A.png" width="420px"/><img src="../../assets/flight_controller/pixhawk6x/hb_6x_internal_v2.png" width="320px"/>

#### Pixhawk 6X (Rev 3/4, 已停产)

<img src="../../assets/flight_controller/pixhawk6x/pixhawk6x_hero_upright.png" width="150px" title="Pixhawk6X 正面图" /> <img src="../../assets/flight_controller/pixhawk6x/pixhawk6x_exploded_diagram.png" width="280px" title="Pixhawk6X 分解图" />

### Pixhawk 6X 基板选项

:::: tabs

::: tab Standard v2A

![Pixhawk 6X Standard v2A](../../assets/flight_controller/pixhawk6x/HB_PH6X_V2A.jpg)

:::

::: tab Standard v2B

![Pixhawk 6X Standard v2B](../../assets/flight_controller/pixhawk6x/HB_PH6X_V2B.jpg)
:::

::: tab Mini

![Pixhawk 6X Mini](../../assets/flight_controller/pixhawk6x/HB_PH6X_Mini.jpg)
:::

::: tab Jetson Baseboard

![Jetson Baseboard](../../assets/flight_controller/pixhawk6x/HB_Jetson_BB.jpg)
:::

::: tab CM4 Baseboard

![Pixhawk 6X CM4](../../assets/flight_controller/pixhawk6x/HB_PH6X_CM4.jpg)
:::

::::

:::tip
此自动驾驶仪得到 PX4 维护和测试团队的[支持](../flight_controller/autopilot_pixhawk_standard.md)。
:::

## 介绍

在 Pixhawk®​ 6X 内部，您可以找到基于 STMicroelectronics​® 的 STM32H753，配对来自 Bosch®​​、InvenSense®​ 的传感器技术，为您提供控制任何自主车辆的灵活性和可靠性，适用于学术和商业应用。

Pixhawk® 6X 的 H7 微控制器包含运行高达 480 MHz 的 Arm® Cortex®-M7 核心，具有 2MB 闪存和 1MB RAM。PX4 Autopilot 利用了增强的功率和 RAM。得益于更新的处理能力，开发人员可以在开发工作中更加高效，允许复杂的算法和模型。

FMUv6X 开放标准包括板载高性能、低噪声 IMU，专为更好的稳定性而设计。三重冗余 IMU 和双重冗余气压计分别在独立总线上。当 PX4 Autopilot 检测到传感器故障时，系统无缝切换到另一个以保持飞行控制可靠性。

独立的 LDO 为每个传感器组供电，具有独立的电源控制。振动隔离系统可滤除高频振动并减少噪声以确保准确读数，使车辆达到更好的整体飞行性能。

外部传感器总线（SPI5）具有两个片选线和数据就绪信号，用于带有 SPI 接口的附加传感器和有效载荷，并且具有集成的 Microchip 以太网 PHY，现在可以通过以太网与任务计算机进行高速通信。

Pixhawk®​ 6X 非常适合企业研究实验室、初创公司、学术界（研究、教授、学生）的开发人员以及商业应用。

## 关键设计要点

- 高性能 STM32H753 处理器
- 模块化飞控：独立的 IMU、FMU 和基础系统，通过 100 针和 50 针 Pixhawk®​ Autopilot Bus 连接器连接。
- 冗余：3x IMU 传感器和 2x 气压计传感器分别在独立总线上
- 三重冗余域：完全隔离的传感器域，具有独立总线和独立电源控制
- 新设计的振动隔离系统，滤除高频振动并减少噪声以确保准确读数
- 用于高速任务计算机集成的以太网接口
- IMU 由板载加热电阻器温控，允许 IMU 的最佳工作温度

### 处理器和传感器

- FMU 处理器：STM32H753
  - 32 位 Arm® Cortex®-M7，480MHz，2MB 闪存，1MB RAM
- IO 处理器：STM32F100
  - 32 位 Arm® Cortex®-M3，24MHz，8KB SRAM
- 板载传感器（当前发货，Rev 8）
  - 加速度计/陀螺仪：3x ICM-45686（具有 BalancedGyro™ 技术）
  - 气压计：ICP20100 和 BMP388
  - 磁力计：BMM150
- 板载传感器（Rev 3/4，已停产）
  - 加速度计/陀螺仪：ICM-20649 或 BMI088
  - 加速度计/陀螺仪：ICM-42688-P
  - 加速度计/陀螺仪：ICM-42670-P
  - 磁力计：BMM150
  - 气压计：2x BMP388

### 电气数据

- 电压额定值：
  - 最大输入电压：6V
  - USB 电源输入：4.75\~5.25V
  - 伺服导轨输入：0\~36V
- 电流额定值：
  - `TELEM1` 输出电流限制器：1.5A
  - 所有其他端口组合输出电流限制器：1.5A

### 机械数据

- 尺寸
  - 飞控模块：38.8 x 31.8 x 14.6mm
  - 标准基板：52.4 x 103.4 x 16.7mm
  - 迷你基板：43.4 x 72.8 x 14.2 mm
- 重量
  - 飞控模块：23g
  - 标准基板：51g
  - 迷你基板：26.5g

### 接口

- 16 个 PWM 伺服输出
- Spektrum / DSM 的 R/C 输入
- PPM 和 S.Bus 输入的专用 R/C 输入
- 专用模拟 / PWM RSSI 输入和 S.Bus 输出
- 4 个通用串行端口
  - 3 个具有完整流控制
  - 1 个具有独立 1.5A 电流限制（Telem1）
  - 1 个具有 I2C 和额外 GPIO 线用于外部 NFC 读取器
- 2 个 GPS 端口
  - 1 个完整的 GPS 加安全开关端口
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

- 其他特性：
  - 工作和存储温度：-40 ~ 85°c

## 购买地址

从 [Holybro](https://holybro.com/products/pixhawk-6x) 订购。

## 组装/设置

[Pixhawk 6X 接线快速入门](../assembly/quick_start_pixhawk6x.md)提供了如何组装所需/重要外设（包括 GPS、电源模块等）的说明。

## 连接

接线图示例
![Pixhawk 6X 接线概览](../../assets/flight_controller/pixhawk6x/pixhawk6x_wiring_diagram.png)

## 引脚定义

- [Holybro Pixhawk 基板引脚定义](https://docs.holybro.com/autopilot/pixhawk-6x/pixhawk-baseboard-pinout)
- [Holybro Pixhawk 迷你基板引脚定义](https://docs.holybro.com/autopilot/pixhawk-6x/pixhawk-mini-baseboard-pinout)
- [Holybro Pixhawk Jetson 基板](https://docs.holybro.com/autopilot/pixhawk-baseboards/pixhawk-jetson-baseboard)
- [Holybro Pixhawk RPi CM4 基板](https://docs.holybro.com/autopilot/pixhawk-baseboards/pixhawk-rpi-cm4-baseboard)

注意：

- [相机捕获引脚](../camera/fc_connected_camera.md#camera-capture-configuration)（`PI0`）是 AD&IO 端口上的引脚 2，在上面标记为 `FMU_CAP1`。

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

[Pixhawk 6X 尺寸](https://docs.holybro.com/autopilot/pixhawk-6x/dimensions)

## 电压额定值

如果提供三个电源，_Pixhawk 6X_ 可以在电源上实现三重冗余。三个电源轨是：**POWER1**、**POWER2** 和 **USB**。Pixhawk 6X 上的 **POWER1** 和 **POWER2** 端口使用 6 路 [2.00mm 间距 CLIK-Mate 线对板 PCB 插座](https://www.molex.com/en-us/products/part-detail/5024430670)。

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

默认启用数字 I2C 电池监控（参见[快速入门 > 电源](../assembly/quick_start_pixhawk6x.md#power)）。

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
make px4_fmu-v6x_default
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

- [遥测无线电模块](https://holybro.com/collections/telemetry-radios?orderby=date)
- [测距仪/距离传感器](../sensor/rangefinders.md)
- [Holybro 传感器](https://holybro.com/collections/sensors)
- [Holybro GPS 和 RTK 系统](https://holybro.com/collections/gps-rtk-systems)
- [电源模块和 PDB](https://holybro.com/collections/power-modules-pdbs)

## 支持的平台/机架

任何可以用正常 RC 伺服或 Futaba S-Bus 伺服控制的多旋翼/飞机/漫游车或船只。完整的支持配置集合可以在[机架参考](../airframes/airframe_reference.md)中看到。

## 更多信息

- [Holybro 文档](https://docs.holybro.com/)（Holybro）
- [Pixhawk 6X 接线快速入门](../assembly/quick_start_pixhawk6x.md)
- [Pixhawk Autopilot FMUv6X 标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-012%20Pixhawk%20Autopilot%20v6X%20Standard.pdf)。
- [Pixhawk Autopilot Bus 标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf)。
- [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。
