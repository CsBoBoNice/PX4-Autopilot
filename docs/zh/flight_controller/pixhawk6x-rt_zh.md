# Holybro Pixhawk 6X-RT

:::warning
PX4 不制造此产品（或任何其他自动驾驶仪）。
如有硬件支持或合规问题，请联系[制造商](https://holybro.com/)。
:::

_Pixhawk 6X-RT_<sup>&reg;</sup> 是成功的 Pixhawk® 飞行控制器系列的最新更新，由 Holybro<sup>&reg;</sup>、NXP 移动机器人团队和 PX4 团队基于 NXP 开源参考设计合作设计和制造。

它基于 [Pixhawk​​® 自动驾驶仪 FMUv6X 标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-012%20Pixhawk%20Autopilot%20v6X%20Standard.pdf)、[自动驾驶仪总线标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf) 和 [连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。

配备高性能 NXP i.mx RT1176 双核处理器、模块化设计、三重冗余、温控 IMU 板、隔离传感器域，提供卓越的性能、可靠性和灵活性。

<img src="../../assets/flight_controller/pixhawk6x-rt/pixhawk6x-rt.png" width="350px" title="Pixhawk6X-RT 正立图" /> <img src="../../assets/flight_controller/pixhawk6x/pixhawk6x_exploded_diagram.png" width="300px" title="Pixhawk6X 分解图" />

:::tip
此自动驾驶仪由 PX4 维护和测试团队[支持](../flight_controller/autopilot_pixhawk_standard.md)。
:::

## 介绍

在 Pixhawk®​ 6X-RT 内部，你可以找到 NXP i.mx RT1176，配合来自 Bosch®​​、InvenSense®​ 的传感器技术，为控制任何自主车辆提供灵活性和可靠性，适用于学术和商业应用。

Pixhawk® 6X-RT 的 i.mx RT1176 跨界双核 MCU 包含运行频率高达 1GHz 的 Arm® Cortex®-M7 内核和运行频率高达 400MHz 的 Arm® Cortex®-M4 内核，具有 2MB SRAM 和 64MB 外部 XIP Flash。
PX4 自动驾驶仪利用了增强的功率和 RAM。
由于处理能力的提升，开发人员可以在开发工作中更高效，支持复杂的算法和模型。

FMUv6X 开放标准包括板载高性能、低噪声 IMU，设计用于更好的稳定性。
在独立总线上三重冗余 IMU 和双重冗余气压计。当 PX4 检测到传感器故障时，系统无缝切换到另一个以保持飞行控制可靠性。

独立 LDO 为每个传感器组供电，具有独立的电源控制。振动隔离系统过滤高频振动并降低噪声以确保准确读数，使车辆达到更好的整体飞行性能。

外部传感器总线（SPI5）有两条片选线和数据就绪信号，用于具有 SPI 接口的附加传感器和有效载荷，配合集成的 Microchip 以太网 PHY，现在可以通过以太网与任务计算机进行高速通信。

Pixhawk®​ 6X-RT 非常适合企业研发实验室、初创公司、学术界（研究、教授、学生）和商业应用的开发人员。

## 主要设计要点

- 高性能 [NXP i.MX RT1170 1GHz 跨界 MCU](https://www.nxp.com/products/i.MX-RT1170)，带 Arm® Cortex® 内核
- 硬件安全元件 [NXP EdgeLock SE051](https://www.nxp.com/products/SE051) 是广受信赖的 EdgeLock SE050 Plug & Trust 安全元件系列的扩展，支持现场小程序更新，提供经过 CC EAL 6+ 认证的可靠安全性，AVA_VAN.5 达到操作系统级别，针对最新攻击场景提供强大保护。例如，安全存储操作员 ID 或证书。
- 模块化飞行控制器：由 100 针和 50 针 Pixhawk®​ 自动驾驶仪总线连接器连接的独立 IMU、FMU 和基础系统。
- 冗余：在独立总线上 3x IMU 传感器和 2x 气压计传感器
- 三重冗余域：完全隔离的传感器域，具有独立总线和独立电源控制
- 新设计的振动隔离系统，过滤高频振动并降低噪声以确保准确读数
- 用于高速任务计算机集成的以太网接口
- IMU 由板载加热电阻器进行温度控制，使 IMU 达到最佳工作温度

### 处理器和传感器

- FMU 处理器：NXP i.MX RT1176
  - 32位 Arm® Cortex®-M7，1GHz
  - 32位 Arm® Cortex®-M4，400MHz 副核
  - 64MB 外部闪存
  - 2MB RAM
- NXP EdgeLock SE051 硬件安全元件
  - IEC62443-4-2 认证，符合适用要求
  - 46 kB 用户存储器，可通过个性化选项扩展至 104 kB
  - 面向物联网部署的突破性 CC EAL6+ 认证解决方案
  - AES 和 3DES 加密和解密
- IO 处理器：STM32F100
  - 32位 Arm® Cortex®-M3，24MHz，8KB SRAM
- 板载传感器
  - 加速度计/陀螺仪：ICM-20649 或 BMI088
  - 加速度计/陀螺仪：ICM-42688-P
  - 加速度计/陀螺仪：ICM-42670-P
  - 磁力计：BMM150
  - 气压计：2x BMP388

### 电气数据

- 电压额定值：
  - 最大输入电压：6V
  - USB 电源输入：4.75~5.25V
  - 舵机导轨输入：0~36V
- 电流额定值：
  - `TELEM1` 输出电流限制器：1.5A
  - 所有其他端口组合输出电流限制器：1.5A

### 机械数据

- 尺寸
  - 飞行控制器模块：38.8 x 31.8 x 14.6mm
  - 标准基板：52.4 x 103.4 x 16.7mm
  - Mini 基板：43.4 x 72.8 x 14.2 mm
- 重量
  - 飞行控制器模块：23g
  - 标准基板：51g
  - Mini 基板：26.5g

### 接口

- 16 路 PWM 舵机输出
- Spektrum / DSM R/C 输入
- 专用 PPM 和 S.Bus 输入 R/C 输入
- 专用模拟/PWM RSSI 输入和 S.Bus 输出
- 4 个通用串行端口
  - 3 个带完整流控制
  - 1 个带独立 1.5A 电流限制（Telem1）
  - 1 个带 I2C 和额外 GPIO 线，用于外部 NFC 读取器
- 2 个 GPS 端口
  - 1 个完整 GPS 加安全开关端口
  - 1 个基本 GPS 端口
- 1 个 I2C 端口
- 1 个以太网端口
  - 无变压器应用
  - 100Mbps
- 1 个 SPI 总线
  - 2 条片选线
  - 2 条数据就绪线
  - 1 条 SPI SYNC 线
  - 1 条 SPI 复位线
- 2 个 CAN 总线用于 CAN 外设
  - CAN 总线具有独立的静默控制或 ESC RX-MUX 控制
- 2 个带 SMBus 的电源输入端口
  - 1 个 AD & IO 端口
  - 2 个额外的模拟输入
  - 1 个 PWM/捕获输入
  - 2 条专用调试和 GPIO 线

- 其他特性：
  - 工作和存储温度：-40 ~ 85°C

## 购买地点

从 [Holybro](https://holybro.com/products/fmuv6x-rt-developer-edition) 订购。

## 组装/设置

[Pixhawk 6X 接线快速入门](../assembly/quick_start_pixhawk6x.md) 提供了如何组装所需/重要外设（包括 GPS、电源模块等）的说明。

## 连接

示例接线图

![Pixhawk 6X 接线概览](../../assets/flight_controller/pixhawk6x/pixhawk6x_wiring_diagram.png)

## 引脚图

- [Holybro Pixhawk 基板引脚图](https://docs.holybro.com/autopilot/pixhawk-6x/pixhawk-baseboard-pinout)
- [Holybro Pixhawk Mini 基板引脚图](https://docs.holybro.com/autopilot/pixhawk-6x/pixhawk-mini-baseboard-pinout)

注意：

- [相机捕获引脚](../camera/fc_connected_camera.md#camera-capture-configuration)（`PI0`）是 AD&IO 端口上的引脚 2，标记为 `FMU_CAP1`。

## 串口映射

| UART   | Device     | Port     |
| ------ | ---------- | -------- |
| UART1  | /dev/ttyS0 | Debug    |
| UART3  | /dev/ttyS1 | GPS      |
| UART4  | /dev/ttyS2 | TELEM1   |
| UART5  | /dev/ttyS3 | GPS2     |
| UART6  | /dev/ttyS4 | PX4IO    |
| UART8  | /dev/ttyS5 | TELEM2   |
| UART10 | /dev/ttyS6 | TELEM3   |
| UART11 | /dev/ttyS7 | External |

## 尺寸

[Pixhawk 6X 尺寸](https://docs.holybro.com/autopilot/pixhawk-6x/dimensions)

## 电压额定值

如果提供三个电源，_Pixhawk 6X-RT_ 可以在电源上实现三重冗余。三个电源导轨是：**POWER1**、**POWER2** 和 **USB**。
Pixhawk 6X 上的 **POWER1** 和 **POWER2** 端口使用 6 回路 [2.00mm 间距 CLIK-Mate 线对板 PCB 插座](https://www.molex.com/en-us/products/part-detail/5024430670)。

**正常操作最大额定值**

在这些条件下，所有电源将按此顺序用于为系统供电：

1. **POWER1** 和 **POWER2** 输入（4.9V 至 5.5V）
1. **USB** 输入（4.75V 至 5.25V）

**绝对最大额定值**

在这些条件下，系统不会汲取任何电力（不会运行），但将保持完整。

1. **POWER1** 和 **POWER2** 输入（操作范围 4.1V 至 5.7V，0V 至 10V 不损坏）
1. **USB** 输入（操作范围 4.1V 至 5.7V，0V 至 6V 不损坏）
1. 舵机输入：**FMU PWM OUT** 和 **I/O PWM OUT** 的 VDD_SERVO 引脚（0V 至 42V 不损坏）

**电压监控**

默认启用数字 I2C 电池监控（参见 [快速入门 > 电源](../assembly/quick_start_pixhawk6x.md#power)）。

::: info
此特定板不支持通过 ADC 进行模拟电池监控，但具有不同基板的此飞行控制器变体可能支持。
:::

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，_QGroundControl_ 会自动安装。
:::

要为此目标[构建 PX4](../dev_setup/building_px4.md)：

```
make px4_fmu-v6xrt_default
```

<a id="debug_port"></a>

## 调试端口

[PX4 系统控制台](../debug/system_console.md)和 [SWD 接口](../debug/swd_debug.md)在 **FMU Debug** 端口上运行。

引脚图和连接器符合 [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)接口中定义的 [Pixhawk Debug Full](../debug/swd_debug.md#pixhawk-debug-full) 接口（JST SM10B 连接器）。

| Pin      | Signal           | Volt  |
| -------- | ---------------- | ----- |
| 1 (red)  | `Vtref`          | +3.3V |
| 2 (blk)  | Console TX (OUT) | +3.3V |
| 3 (blk)  | Console RX (IN)  | +3.3V |
| 4 (blk)  | `SWDIO`          | +3.3V |
| 5 (blk)  | `SWCLK`          | +3.3V |
| 6 (blk)  | `SWO`            | +3.3V |
| 7 (blk)  | NFC GPIO         | +3.3V |
| 8 (blk)  | PH11             | +3.3V |
| 9 (blk)  | nRST             | +3.3V |
| 10 (blk) | `GND`            | GND   |

有关使用此端口的信息，请参阅：

- [SWD 调试端口](../debug/swd_debug.md)
- [PX4 系统控制台](../debug/system_console.md)（注意，FMU 控制台映射到 USART3）。

## 外设

- [数字空速传感器](https://holybro.com/products/digital-air-speed-sensor-ms4525do)
- [遥测无线电模块](https://holybro.com/collections/telemetry-radios?orderby=date)
- [测距仪/距离传感器](../sensor/rangefinders.md)

## 支持的平台/机架

任何可以用普通 RC 舵机或 Futaba S-Bus 舵机控制的多旋翼/飞机/地面车辆或船舶。
完整的支持配置集合可以在[机架参考](../airframes/airframe_reference.md)中看到。

## 更多信息

- [更新 Pixhawk 6X-RT Bootloader](../advanced_config/bootloader_update_v6xrt.md)
- [Holybro 文档](https://docs.holybro.com/)（Holybro）
- [Pixhawk 6X 接线快速入门](../assembly/quick_start_pixhawk6x.md)
- [PM02D 电源模块](../power_module/holybro_pm02d.md)
- [PM03D 电源模块](../power_module/holybro_pm03d.md)
- [Pixhawk 自动驾驶仪 FMUv6X 标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-012%20Pixhawk%20Autopilot%20v6X%20Standard.pdf)。
- [Pixhawk 自动驾驶仪总线标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf)。
- [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。
