# Holybro Pixhawk 6C Mini

:::warning
PX4 不制造此产品（或任何其他自动驾驶仪）。
如有硬件支持或合规问题，请联系[制造商](https://holybro.com/)。
:::

_Pixhawk 6C Mini_<sup>&reg;</sup> 是成功的 Pixhawk® 飞行控制器系列的最新更新，由 Holybro<sup>&reg;</sup> 与 PX4 团队合作设计和制造。

它配备高性能 H7 处理器，具有 IMU 冗余、温控 IMU 板和成本效益设计，提供卓越的性能和可靠性。
它符合 Pixhawk [连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。

![Pixhawk6c mini A&B 图像](../../assets/flight_controller/pixhawk6c_mini/HB_6C_MINI-A_B.jpg)

:::tip
此自动驾驶仪由 PX4 维护和测试团队[支持](../flight_controller/autopilot_pixhawk_standard.md)。
:::

## 介绍

Pixhawk® 6C Mini 是成功的 Pixhawk® 飞行控制器系列的最新更新。

在 Pixhawk® 6C Mini 内部，你可以找到基于 STMicroelectronics® 的 STM32H743，配合来自 Bosch® 和 InvenSense® 的传感器技术，为控制任何自主车辆提供灵活性和可靠性，适用于学术和商业应用。

Pixhawk® 6C Mini 的 H7 微控制器包含运行频率高达 480 MHz 的 Arm® Cortex®-M7 内核，具有 2MB 闪存和 1MB RAM。
由于处理能力的提升，开发人员可以在开发工作中更高效，支持复杂的算法和模型。

Pixhawk 6C Mini 板载高性能、低噪声 IMU，设计为成本效益的同时具有 IMU 冗余。
振动隔离系统用于过滤高频振动并降低噪声以确保准确读数，使车辆达到更好的整体飞行性能。

Pixhawk® 6C Mini 非常适合企业研发实验室、初创公司、学术界（研究、教授、学生）和商业应用的开发人员。

**主要设计要点**

- 高性能 STM32H743 处理器，具有更强的计算能力和 RAM
- 新的成本效益设计，采用低轮廓外形
- 新设计的集成振动隔离系统，过滤高频振动并降低噪声以确保准确读数
- IMU 由板载加热电阻器进行温度控制，使 IMU 达到最佳工作温度

## 技术规格

### **处理器和传感器**

- FMU 处理器：STM32H743
  - 32位 Arm® Cortex®-M7，480MHz，2MB 内存，1MB SRAM
- IO 处理器：STM32F103
  - 32位 Arm® Cortex®-M3，72MHz，64KB SRAM
- 板载传感器
  - 加速度计/陀螺仪：ICM-42688-P
  - 加速度计/陀螺仪：BMI055
  - 磁力计：IST8310
  - 气压计：MS5611

### **电气数据**

- 电压额定值：
  - 最大输入电压：6V
  - USB 电源输入：4.75~5.25V
  - 舵机导轨输入：0~36V
- 电流额定值：
  - `TELEM1` 最大输出电流限制器：1A
  - 所有其他端口组合输出电流限制器：1A

### **机械数据**

- 尺寸：53.3 x 39 x 16.2 mm
- 重量：39.2g

### **接口**

- 14 路 PWM 舵机输出（8 路来自 IO，6 路来自 FMU）
- 3 个通用串行端口
  - `TELEM1` - 全流控制，独立 1A 电流限制
  - `TELEM2` - 全流控制
- 2 个 GPS 端口
  - GPS1 - 完整 GPS 端口（GPS 加安全开关）
  - GPS2 - 基本 GPS 端口
- 1 个 I2C 端口
  - 支持位于传感器模块上的专用 I2C 校准 EEPROM
- 2 个 CAN 总线
  - CAN 总线具有独立的静默控制或 ESC RX-MUX 控制
- 1 个调试端口：
  - FMU 调试 Mini
- 专用 R/C 输入，用于 Spektrum/DSM 和 S.BUS、CPPM、模拟/PWM RSSI
- 1 个电源输入端口（模拟）

- 其他特性：
  - 工作和存储温度：-40 ~ 85°C

## 购买地点

从 [Holybro](https://holybro.com/products/pixhawk-6c-mini) 订购。

## 组装/设置

Pixhawk 4 Mini 的端口与 Pixhawk 6C Mini 的端口非常相似。
请参考 [Pixhawk 4 Mini 接线快速入门](../assembly/quick_start_pixhawk4_mini.md)，它提供了如何组装所需/重要外设（包括 GPS、电源模块等）的说明。

## 引脚图

- [Holybro Pixhawk 6C Mini 端口引脚图](https://docs.holybro.com/autopilot/pixhawk-6c-mini/pixhawk-6c-mini-ports)

## 串口映射

| UART   | Device     | QGC 参数描述   | FC 上的端口标签 |
| ------ | ---------- | ------------- | -------------- |
| USART1 | /dev/ttyS0 | GPS1          | GPS1           |
| USART2 | /dev/ttyS1 | TELEM3        | N/A            |
| USART3 | /dev/ttyS2 | N/A           | FMU Debug      |
| UART5  | /dev/ttyS3 | TELEM2        | TELEM2         |
| USART6 | /dev/ttyS4 | PX4IO         | I/O PWM Out    |
| UART7  | /dev/ttyS5 | TELEM1        | TELEM1         |
| UART8  | /dev/ttyS6 | GPS2          | GPS2           |

<!-- See https://docs.px4.io/main/en/hardware/serial_port_mapping.html#serial-port-mapping -->

## 尺寸

![Pixhawk6c Mini A 尺寸](../../assets/flight_controller/pixhawk6c_mini/pixhawk_6c_mini_dimension.jpg)
![Pixhawk6c Mini B 尺寸](../../assets/flight_controller/pixhawk6c_mini/pixhawk_6c_mini_b_dimensions.jpg)

## 电压额定值

如果提供两个电源，_Pixhawk 6C Mini_ 可以在电源上实现双重冗余。两个电源导轨是：**POWER1** 和 **USB**。

**正常操作最大额定值**

在这些条件下，所有电源将按此顺序用于为系统供电：

1. **POWER1** 输入（4.9V 至 5.5V）
1. **USB** 输入（4.75V 至 5.25V）

**绝对最大额定值**

在这些条件下，系统不会汲取任何电力（不会运行），但将保持完整。

1. **POWER1** 输入（操作范围 4.1V 至 5.7V，0V 至 10V 不损坏）
1. **USB** 输入（操作范围 4.1V 至 5.7V，0V 至 6V 不损坏）
1. 舵机输入：**FMU PWM OUT** 和 **I/O PWM OUT** 的 VDD_SERVO 引脚（0V 至 42V 不损坏）

**电压监控**

Pixhawk 6C Mini 使用模拟电源模块。

Holybro 为不同需求制造各种模拟[电源模块](../power_module/index.md)：

- [PM02 电源模块](../power_module/holybro_pm02.md)
- [PM06 电源模块](../power_module/holybro_pm06_pixhawk4mini_power_module.md)
- [PM07 电源模块](../power_module/holybro_pm07_pixhawk4_power_module.md)
- [PM08 电源模块](https://holybro.com/products/pm08-power-module-14s-200a)

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，_QGroundControl_ 会自动安装。
:::

要为此目标[构建 PX4](../dev_setup/building_px4.md)：

```
make px4_fmu-v6c_default
```

<a id="debug_port"></a>

## 调试端口

[PX4 系统控制台](../debug/system_console.md)和 [SWD 接口](../debug/swd_debug.md)在 **FMU Debug** 端口上运行。

引脚图和连接器符合 [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)接口中定义的 [Pixhawk Debug Mini](../debug/swd_debug.md#pixhawk-debug-mini) 接口（JST SH 连接器）。

| Pin     | Signal           | Volt  |
| ------- | ---------------- | ----- |
| 1 (red) | `Vtref`          | +3.3V |
| 2 (blk) | Console TX (OUT) | +3.3V |
| 3 (blk) | Console RX (IN)  | +3.3V |
| 4 (blk) | `SWDIO`          | +3.3V |
| 5 (blk) | `SWCLK`          | +3.3V |
| 6 (blk) | `GND`            | GND   |

有关使用此端口的信息，请参阅：

- [SWD 调试端口](../debug/swd_debug.md)
- [PX4 系统控制台](../debug/system_console.md)（注意，FMU 控制台映射到 USART3）。

## 外设

- [数字空速传感器](https://holybro.com/products/digital-air-speed-sensor-ms4525do)
- [遥测无线电模块](../telemetry/index.md)：
  - [Holybro 遥测无线电](../telemetry/holybro_sik_radio.md)
  - [Holybro Microhard P900 无线电](../telemetry/holybro_microhard_p900_radio.md)
  - [Holybro XBP9X 遥测无线电](../telemetry/holybro_xbp9x_radio.md)
- [测距仪/距离传感器](../sensor/rangefinders.md)

## 支持的平台/机架

任何可以用普通 RC 舵机或 Futaba S-Bus 舵机控制的多旋翼/飞机/地面车辆或船舶。
完整的支持配置集合可以在[机架参考](../airframes/airframe_reference.md)中看到。

## 另请参阅

- [Holybro 文档](https://docs.holybro.com/)（Holybro）
- [Pixhawk 4 Mini 接线快速入门](../assembly/quick_start_pixhawk4_mini.md)（和 [Pixhawk 6C 接线快速入门](../assembly/quick_start_pixhawk6c.md)）
- [PM02 电源模块](../power_module/holybro_pm02.md)
- [PM06 电源模块](../power_module/holybro_pm06_pixhawk4mini_power_module.md)
- [PM07 电源模块](../power_module/holybro_pm07_pixhawk4_power_module.md)
- [PM08 电源模块](https://holybro.com/products/pm08-power-module-14s-200a)
- [FMUv6C 参考设计引脚图](https://docs.google.com/spreadsheets/d/1FcmWRKd6zjdz3-cnjEDYEmANKZOFzNSc/edit?usp=sharing&ouid=113251442407318461574&rtpof=true&sd=true)。
- [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。
