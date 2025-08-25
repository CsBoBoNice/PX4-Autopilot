# Holybro Pixhawk 6C

:::warning
PX4不制造此飞控（或任何其他自动驾驶仪）。
如需硬件支持或合规问题，请联系[制造商](https://holybro.com/)。
:::

_Pixhawk 6C_<sup>&reg;</sup> 是成功的 Pixhawk® 飞控系列的最新更新，由 Holybro<sup>&reg;</sup> 与 PX4 团队协作设计和制造。

它配备高性能 H7 处理器，具有 IMU 冗余、温控 IMU 板和成本效益设计，提供令人难以置信的性能和可靠性。它符合 Pixhawk [连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。

<img src="../../assets/flight_controller/pixhawk6c/pixhawk6c_hero_upright.png" width="250px" title="Pixhawk6c 正面图" />

:::tip
此自动驾驶仪得到 PX4 维护和测试团队的[支持](../flight_controller/autopilot_pixhawk_standard.md)。
:::

## 介绍

Pixhawk® 6C 是成功的 Pixhawk® 飞控系列的最新更新。

在 Pixhawk® 6C 内部，您可以找到基于 STMicroelectronics® 的 STM32H743，配对来自 Bosch® 和 InvenSense® 的传感器技术，为您提供控制任何自主车辆的灵活性和可靠性，适用于学术和商业应用。

Pixhawk® 6C 的 H7 微控制器包含运行高达 480 MHz 的 Arm® Cortex®-M7 核心，具有 2MB 闪存和 1MB RAM。得益于更新的处理能力，开发人员可以在开发工作中更加高效，允许复杂的算法和模型。

Pixhawk 6C 包括板载高性能、低噪声 IMU，专为成本效益而设计，同时具有 IMU 冗余。振动隔离系统可滤除高频振动并减少噪声以确保准确读数，使车辆达到更好的整体飞行性能。

Pixhawk® 6C 非常适合企业研究实验室、初创公司、学术界（研究、教授、学生）的开发人员以及商业应用。

**关键设计要点**

- 高性能 STM32H743 处理器，具有更多计算能力和 RAM
- 新的成本效益设计，具有低轮廓外形
- 新设计的集成振动隔离系统，滤除高频振动并减少噪声以确保准确读数
- IMU 由板载加热电阻器温控，允许 IMU 的最佳工作温度

# 技术规格

### **处理器和传感器**

- FMU 处理器：STM32H743
  - 32 位 Arm® Cortex®-M7，480MHz，2MB 内存，1MB SRAM
- IO 处理器：STM32F103
  - 32 位 Arm® Cortex®-M3，72MHz，64KB SRAM
- 板载传感器
  - 加速度计/陀螺仪：ICM-42688-P
  - 加速度计/陀螺仪：BMI055
  - 磁力计：IST8310
  - 气压计：MS5611

### **电气数据**

- 电压额定值：
  - 最大输入电压：6V
  - USB 电源输入：4.75\~5.25V
  - 伺服导轨输入：0\~36V
- 电流额定值：
  - TELEM1 最大输出电流限制器：1.5A
  - 所有其他端口组合输出电流限制器：1.5A

### **机械数据**

- 尺寸：84.8 \* 44 \* 12.4 mm
- 重量：59.3g

### **接口**

- 16 个 PWM 伺服输出（8 个来自 IO，8 个来自 FMU）
- 3 个通用串行端口
  - TELEM1 - 完整流控制，独立 1.5A 电流限制
  - TELEM2 - 完整流控制
  - TELEM3
- 2 个 GPS 端口
  - GPS1 - 完整 GPS 端口（GPS 加安全开关）
  - GPS2 - 基本 GPS 端口
- 1 个 I2C 端口
  - 支持位于传感器模块上的专用 I2C 校准 EEPROM
- 2 个 CAN 总线
  - CAN 总线具有独立静音控制或 ESC RX-MUX 控制
- 2 个调试端口：
  - FMU 调试
  - I/O 调试
- Spektrum / DSM 和 S.BUS、CPPM、模拟 / PWM RSSI 的专用 R/C 输入
- 专用 S.BUS 输出
- 2 个电源输入端口（模拟）

- 其他特性：
  - 工作和存储温度：-40 ~ 85°c

## 购买地址

从 [Holybro](https://holybro.com/products/pixhawk-6c) 订购。

## 组装/设置

[Pixhawk 6C 接线快速入门](../assembly/quick_start_pixhawk6c.md)提供了如何组装所需/重要外设（包括 GPS、电源模块等）的说明。

## 引脚定义

- [Holybro Pixhawk 6C 引脚定义](https://docs.holybro.com/autopilot/pixhawk-6c/pixhawk-6c-pinout)

## 串口映射

| UART   | 设备         | 端口            |
| ------ | ---------- | ------------- |
| USART1 | /dev/ttyS0 | GPS1          |
| USART2 | /dev/ttyS1 | TELEM3        |
| USART3 | /dev/ttyS2 | 调试控制台         |
| UART5  | /dev/ttyS3 | TELEM2        |
| USART6 | /dev/ttyS4 | PX4IO         |
| UART7  | /dev/ttyS5 | TELEM1        |
| UART8  | /dev/ttyS6 | GPS2          |

## 尺寸

- [Pixhawk 6C 尺寸](https://docs.holybro.com/autopilot/pixhawk-6c/dimensions)

## 电压额定值

如果提供三个电源，_Pixhawk 6C_ 可以在电源上实现三重冗余。三个电源轨是：**POWER1**、**POWER2** 和 **USB**。

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

Pixhawk 6C 使用模拟电源模块。

Holybro 为不同需求制造各种模拟[电源模块](../power_module/index.md)：

- [PM02 电源模块](../power_module/holybro_pm02.md)
- [PM06 电源模块](../power_module/holybro_pm06_pixhawk4mini_power_module.md)
- [PM07 电源模块](../power_module/holybro_pm07_pixhawk4_power_module.md)

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时由 _QGroundControl_ 自动安装。
:::

为此目标[构建 PX4](../dev_setup/building_px4.md)：

```
make px4_fmu-v6c_default
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

- [Holybro 文档](https://docs.holybro.com/)（Holybro）
- [Pixhawk 6C 接线快速入门](../assembly/quick_start_pixhawk6c.md)
- [PM02 电源模块](../power_module/holybro_pm02.md)
- [PM06 电源模块](../power_module/holybro_pm06_pixhawk4mini_power_module.md)
- [PM07 电源模块](../power_module/holybro_pm07_pixhawk4_power_module.md)
- [FMUv6C 参考设计引脚定义](https://docs.google.com/spreadsheets/d/1FcmWRKd6zjdz3-cnjEDYEmANKZOFzNSc/edit?usp=sharing&ouid=113251442407318461574&rtpof=true&sd=true)。
- [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。
