# NXP MR-VMU-RT1176 飞控

<Badge type="tip" text="PX4 v1.15" />

:::warning
PX4不制造此飞控（或任何其他自动驾驶仪）。
如需硬件支持（https://community.nxp.com/）或合规问题，请联系[制造商](https://www.nxp.com)。
:::

_MR-VMU-RT1176_ 参考设计基于 [Pixhawk<sup>&reg;</sup> FMUv6X-RT 开放标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-020%20Pixhawk%20Autopilot%20v6X-RT%20Standard.pdf)，这是成功的 Pixhawk<sup>&reg;</sup> 飞控系列的最新更新。

这是 NXP 使用 FMUv6X-RT 的开源_参考设计_，由工业合作伙伴<sup>&reg;</sup>、NXP 移动机器人团队和 PX4 团队协作设计和制造。作为参考/评估设计，它旨在被其他人复制、修改或批量生产集成。它已经通过了所有 FCC/CE ROHS REACH UKCA、EMI/RFI ESD 认证，并在全球范围内可用。多家第三方制造商（如 Holybro.com）提供此产品或衍生商业产品。

![MR-VMU-RT1176 正面图](../../assets/flight_controller/nxp_mr-vmu-rt1176/mr-vmu-rt1176_upleft.jpg)

该板包含与 Pixhawk 6X-RT 上相同的 FMU 模块，配对基于 NXP 的载板。载板提供 100Base-T1（两线）汽车以太网、NFC 天线（连接到 SE051）和第三个 CAN 总线。它还移除了 IO 处理器以启用 12 个 PWM 端口，其中 8 个提供 Dshot 功能。

该板利用了多个 Pixhawk​​® 开放标准，如 FMUv6X-RT 标准、[自动驾驶仪总线标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf)和[连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。配备高性能 NXP i.mx RT1176 双核处理器、模块化设计、三重冗余、温控 IMU 板、隔离传感器域，提供令人难以置信的性能、可靠性和灵活性。

:::tip
此自动驾驶仪得到 PX4 维护和测试团队的[支持](../flight_controller/autopilot_pixhawk_standard.md)。
:::

## 介绍

在 MR-VMU-RT1176 内部，您可以找到 NXP i.MX RT1176，配对来自 Bosch®、InvenSense® 的传感器技术，为您提供控制任何自主车辆的灵活性和可靠性，适用于学术和商业应用。

Pixhawk® 6X-RT 的 i.MX RT1176 Crossover 双核 MCU 包含运行高达 1GHz 的 Arm® Cortex®-M7 核心和运行高达 400MHz 的 Arm® Cortex®-M4 核心，具有 2MB SRAM 和 64MB 外部 XIP Flash。PX4 自动驾驶仪利用了增强的处理能力和 RAM。得益于增强的处理能力，开发人员可以在开发工作中更加高效，允许复杂的算法和模型。

FMUv6X-RT 开放标准包括板载高性能、低噪声 IMU，专为更好的稳定性而设计。三重冗余 IMU 和双重冗余气压计分别在独立总线上。当 PX4 检测到传感器故障时，系统无缝切换到另一个以保持飞行控制可靠性。

独立的 LDO 为每个传感器组供电，具有独立的电源控制。独立的振动隔离系统可滤除高频振动并减少噪声以确保准确读数，使车辆达到更好的整体飞行性能。

外部传感器总线（SPI5）具有两个片选线和数据就绪信号，用于带有 SPI 接口的附加传感器和有效载荷，并且具有集成的 Microchip 以太网 PHY，现在可以通过以太网与任务计算机进行高速通信。

MR-VMU-RT1176 参考设计非常适合企业研究实验室、初创公司、学术界（研究、教授、学生）的开发人员以及想要尝试 T1（2 线）汽车以太网的商业应用。

请注意，由于这是一个参考设计，这个_特定_板不会大批量生产。我们的被许可方将提供类似的变体。

## 关键设计要点

- 高性能 [NXP i.MX RT1170 1GHz Crossover MCU](https://www.nxp.com/products/i.MX-RT1170)，具有 Arm® Cortex® 核心
- 硬件安全元件 [NXP EdgeLock SE051](https://www.nxp.com/products/SE051)。这是广受信赖的 EdgeLock SE050 Plug & Trust 安全元件系列的扩展，支持现场小程序更新，并提供经 CC EAL 6+ 认证的成熟安全性，AVA_VAN.5 达到 OS 级别，可强力防护最新的攻击场景。例如，这可用于安全存储操作员 ID 或证书。
- 模块化飞控：独立的 IMU、FMU 和基础系统，通过 100 针和 50 针 Pixhawk® 自动驾驶仪总线连接器连接。
- 冗余：3x IMU 传感器和 2x 气压计传感器分别在独立总线上
- 三重冗余域：完全隔离的传感器域，具有独立总线和独立电源控制
- 新设计的振动隔离系统，滤除高频振动并减少噪声以确保准确读数
- 100Base-T1 2 线以太网接口，用于高速任务计算机集成
- IMU 由板载加热电阻器温控，允许 IMU 的最佳工作温度

### 处理器和传感器

- FMU 处理器：NXP i.MX RT1176
  - 32 位 Arm® Cortex®-M7，1GHz
  - 32 位 Arm® Cortex®-M4，400MHz 辅助核心
  - 64MB 外部闪存
  - 2MB RAM
- NXP EdgeLock SE051 硬件安全元件
  - IEC62443-4-2 认证适用的要求
  - 46 kB 用户内存，个性化选项可达 104 kB
  - 突破性的 CC EAL6+ 认证解决方案用于 IoT 部署
  - AES 和 3DES 加密和解密
- 板载传感器
  - 加速度计/陀螺仪：ICM-20649 或 BMI088
  - 加速度计/陀螺仪：ICM-42688-P
  - 加速度计/陀螺仪：ICM-42670-P
  - 磁力计：BMM150
  - 气压计：2x BMP388

### 电气数据

- 电压额定值：
  - 最大输入电压：6V
  - USB 电源输入：4.75\~5.25V
  - 舵机电源输入：0\~36V
- 电流额定值：
  - `TELEM1` 输出电流限制器：1.5A
  - 所有其他端口组合输出电流限制器：1.5A

### 机械数据

- 尺寸
  - 飞控模块：38.8 x 31.8 x 14.6mm
  - 标准基板：50 x 96 x 16.7mm
- 重量
  - 飞控模块：23g
  - 标准基板：51g

### 接口

- 12 个 PWM 舵机输出，8 个具有 D-SHOT
- Spektrum / DSM 的 R/C 输入
- PPM 和 S.Bus 输入的专用 R/C 输入
- 专用模拟 / PWM RSSI 输入和 S.Bus 输出
- 4 个通用串行端口：
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
- 3 个 CAN 总线用于 CAN 外设（PX4 目前支持 2 个）
  - CAN 总线具有独立静音控制或 ESC RX-MUX 控制
- 2 个具有 SMBus 的电源输入端口
- 1 个 AD & IO 端口
- 2 个额外模拟输入
- 1 个 PWM/捕获输入
- 2 个专用调试和 GPIO 线

- 其他特性：
  - 工作和存储温度：-40 ~ 85°c

## 购买地址

可从 [NXP](https://www.nxp.com) 订购。

## 组装/设置

接线类似于 [Holybro Pixhawk 6X](../flight_controller/pixhawk6x.md#connections) 和其他遵循 [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)的板。

<!-- TBD - provide sample wiring diagram. -->

## 连接

_MR-VMU-RT1176_ 连接器（遵循 [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)）

![MR-VMU-RT1176 顶部图](../../assets/flight_controller/nxp_mr-vmu-rt1176/mr-vmu-rt1176_top.jpg)
![MR-VMU-RT1176 前面图](../../assets/flight_controller/nxp_mr-vmu-rt1176/mr-vmu-rt1176_front.jpg)
![MR-VMU-RT1176 左侧图](../../assets/flight_controller/nxp_mr-vmu-rt1176/mr-vmu-rt1176_left.jpg)
![MR-VMU-RT1176 右侧图](../../assets/flight_controller/nxp_mr-vmu-rt1176/mr-vmu-rt1176_right.jpg)

更多信息请参阅：

- [NXP MR-VMU-RT1176 基板连接](https://nxp.gitbook.io/vmu-rt1176/production-v1-carrier-board-connectors) (nxp.gitbook.io)

## 引脚定义

[NXP MR-VMU-RT1176 基板引脚定义](https://nxp.gitbook.io/vmu-rt1176/pin-out) (nxp.gitbook.io)

注意：

- [相机捕获引脚](../camera/fc_connected_camera.md#camera-capture-configuration)（`PI0`）是 AD&IO 端口上的引脚 2，在上面标记为 `FMU_CAP1`。

## 串口映射

| UART   | 设备       | 端口     |
| ------ | ---------- | -------- |
| UART1  | /dev/ttyS0 | 调试     |
| UART3  | /dev/ttyS1 | GPS      |
| UART4  | /dev/ttyS2 | TELEM1   |
| UART5  | /dev/ttyS3 | GPS2     |
| UART6  | /dev/ttyS4 | PX4IO    |
| UART8  | /dev/ttyS5 | TELEM2   |
| UART10 | /dev/ttyS6 | TELEM3   |
| UART11 | /dev/ttyS7 | 外部     |

<!--
## Dimensions

TBD
-->

## 电压额定值

如果提供三个电源，_MR-VMU-RT1176_ 可以在电源上实现三重冗余。三个电源轨是：**POWER1**、**POWER2** 和 **USB**。MR-VMU-RT1176 上的 **POWER1** 和 **POWER2** 端口使用 6 路 [2.00mm 间距 CLIK-Mate 线对板 PCB 插座](https://www.molex.com/en-us/products/part-detail/5024430670)。

### 正常操作最大额定值

在这些条件下，所有电源将按以下顺序为系统供电：

1. **POWER1** 和 **POWER2** 输入（4.9V 至 5.5V）
1. **USB** 输入（4.75V 至 5.25V）

### 绝对最大额定值

在这些条件下，系统不会吸取任何电力（不会工作），但会保持完整。

1. **POWER1** 和 **POWER2** 输入（工作范围 4.1V 至 5.7V，0V 至 10V 无损坏）
1. **USB** 输入（工作范围 4.1V 至 5.7V，0V 至 6V 无损坏）
1. 舵机输入：**FMU PWM OUT** 和 **I/O PWM OUT** 的 VDD_SERVO 引脚（0V 至 42V 无损坏）

### 电压监控

默认启用数字 I2C 电池监控（参见 [快速入门 > 电源](../assembly/quick_start_pixhawk6x.md#power)）。

::: info
此特定板不支持通过 ADC 进行模拟电池监控，但在具有不同基板的此飞控变体中可能受支持。
:::

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时由 _QGroundControl_ 自动安装。
:::

为此目标[构建 PX4](../dev_setup/building_px4.md)：

```sh
make px4_fmu-v6xrt_default
```

## 调试端口 {#debug_port}

[PX4 系统控制台](../debug/system_console.md)和 [SWD 接口](../debug/swd_debug.md)在 **FMU Debug** 端口上运行。

引脚定义和连接器符合在 [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)接口中定义的 [Pixhawk Debug Full](../debug/swd_debug.md#pixhawk-debug-full) 接口（JST SM10B 连接器）。

| 引脚     | 信号             | 电压  |
| -------- | ---------------- | ----- |
| 1 (红)   | `Vtref`          | +3.3V |
| 2 (黑)   | 控制台 TX (OUT)  | +3.3V |
| 3 (黑)   | 控制台 RX (IN)   | +3.3V |
| 4 (黑)   | `SWDIO`          | +3.3V |
| 5 (黑)   | `SWCLK`          | +3.3V |
| 6 (黑)   | `SWO`            | +3.3V |
| 7 (黑)   | NFC GPIO         | +3.3V |
| 8 (黑)   | PH11             | +3.3V |
| 9 (黑)   | nRST             | +3.3V |
| 10 (黑)  | `GND`            | GND   |

有关使用此端口的信息，请参阅：

- [SWD 调试端口](../debug/swd_debug.md)
- [PX4 系统控制台](../debug/system_console.md)（注意，FMU 控制台映射到 USART3）。

## 外设

- [数字空速传感器](https://holybro.com/products/digital-air-speed-sensor-ms4525do)
- [遥测无线电模块](https://holybro.com/collections/telemetry-radios?orderby=date)
- [测距仪/距离传感器](../sensor/rangefinders.md)

## 支持的平台/机架

任何可以用正常 RC 舵机或 Futaba S-Bus 舵机控制的多旋翼/飞机/漫游车或船只。完整的支持配置集合可以在[机架参考](../airframes/airframe_reference.md)中看到。

## 更多信息

- [更新 Pixhawk 6X-RT 引导加载程序](../advanced_config/bootloader_update_v6xrt.md)
- [Pixhawk 6X 接线快速入门](../assembly/quick_start_pixhawk6x.md)
- [PM02D 电源模块](../power_module/holybro_pm02d.md)
- [PM03D 电源模块](../power_module/holybro_pm03d.md)
- [Pixhawk FMUv6X-RT 开放标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-020%20Pixhawk%20Autopilot%20v6X-RT%20Standard.pdf)
- [Pixhawk 自动驾驶仪总线标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf)。
- [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。
