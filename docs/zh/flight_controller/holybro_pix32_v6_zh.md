# Holybro Pix32 v6

:::warning
PX4 不制造此（或任何）自驾仪。
如需硬件支持或合规问题，请联系[制造商](https://holybro.com/)。
:::

_Pix32 v6_<sup>&reg;</sup> 是 pix32 v5 飞行控制器的最新更新版本。它是 Pixhawk 6C 的变体，采用模块化设计并共享相同的 FMUv6C 目标。它由独立的飞行控制器和载板组成，通过 [100 引脚连接器](https://docs.holybro.com/autopilot/pix32-v6/download) 连接。它专为需要高功率、灵活和可定制飞行控制系统的飞行员而设计。

它配备了高性能 H7 处理器，具有 IMU 冗余、温控 IMU 板和经济高效的设计，提供令人难以置信的性能和可靠性。它符合[连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。

<img src="../../assets/flight_controller/pix32v6/pix32v6_fc_only.png" width="550px" title="pix32v6 正视图" />

<!--
:::tip
此自驾仪由 PX4 维护和测试团队[支持](../flight_controller/autopilot_pixhawk_standard.md)。
:::
-->

## 介绍

在 Pix32 v6 内部，您可以找到基于 STMicroelectronics® 的 STM32H743，与来自 Bosch® 和 InvenSense® 的传感器技术配对，为控制任何自主飞行器提供灵活性和可靠性，适用于学术和商业应用。

Pix32 v6 的 H7 MCU 包含运行高达 480 MHz 的 Arm® Cortex®-M7 内核，具有 2MB 闪存和 1MB RAM。借助更新的处理能力，开发人员可以在开发工作中更加高效，允许复杂的算法和模型。它包括板载高性能、低噪声 IMU，设计为经济高效的同时具有 IMU 冗余。振动隔离系统过滤高频振动并降低噪声以确保准确读数，使飞行器达到更好的整体飞行性能。

这款飞行控制器非常适合寻找可使用定制基板的经济实惠且模块化飞行控制器的用户。我们已经公开了 [pix32 v6 基板原理图](https://docs.holybro.com/autopilot/pix32-v6/download)，您可以自己制作定制载板或让我们帮助您。通过使用定制基板，您可以确保物理尺寸、引脚分布和功率分配要求与您的飞行器完美匹配，确保您拥有所需的所有连接，而没有不需要的连接器的费用和体积。

**关键设计要点**

- 高性能 STM32H743 处理器，具有更多计算能力和 RAM
- 新的经济高效设计，采用低轮廓外形
- 集成振动隔离系统，过滤高频振动并降低噪声以确保准确读数
- IMU 由板载加热电阻器进行温度控制，允许 IMU 的最佳工作温度

# 技术规格

### **处理器和传感器**

- FMU 处理器：STM32H743&#x20;
  - 32 位 Arm® Cortex®-M7，480MHz，2MB 内存，1MB SRAM&#x20;
- IO 处理器：STM32F103
  - &#x20;32 位 Arm® Cortex®-M3，72MHz，64KB SRAM&#x20;
- 板载传感器&#x20;
  - &#x20;加速度计/陀螺仪：ICM-42688-P&#x20;
  - 加速度计/陀螺仪：BMI055&#x20;
  - 磁力计：IST8310&#x20;
  - 气压计：MS5611

### **电气数据**

- 电压额定值：
  - 最大输入电压：6V
  - USB 电源输入：4.75\~5.25V
  - 舵机轨输入：0\~36V
- 电流额定值：
  - TELEM1 最大输出电流限制器：1.5A
  - 所有其他端口组合输出电流限制器：1.5A

### **机械数据**

- FC 模块尺寸：44.8 x 44.8 x 13.5
- FC 模块重量：36g

### **接口**

- 16 个 PWM 舵机输出（8 个来自 IO，8 个来自 FMU）
- 3 个通用串行端口
  - `TELEM1` - 完整流量控制，独立 1.5A 电流限制
  - `TELEM2` - 完整流量控制
  - `TELEM3`
- 2 个 GPS 端口
  - `GPS1` - 完整 GPS 端口（GPS 加安全开关）
  - `GPS2` - 基本 GPS 端口
- 1 个 I2C 端口
  - 支持位于传感器模块上的专用 I2C 校准 EEPROM
- 2 个 CAN 总线
  - CAN 总线具有独立的静默控制或 ESC RX-MUX 控制
- 2 个调试端口：
  - FMU 调试
  - I/O 调试
- Spektrum / DSM 和 S.BUS、CPPM、模拟 / PWM RSSI 专用 R/C 输入
- 专用 S.BUS 输出
- 2 个电源输入端口（模拟）

- 其他特性：
  - 工作和存储温度：-40 ~ 85°c

## 购买渠道

从 [Holybro](https://holybro.com/products/pix32-v6) 订购。

## 引脚分布

- [Holybro Pix32 v6 基板端口引脚分布](https://docs.holybro.com/autopilot/pix32-v6/pix32-v6-baseboard-ports)
- [Holybro Pix32 v6 基板端口引脚分布](https://docs.holybro.com/autopilot/pix32-v6/pix32-v6-mini-base-ports)

## 串口映射

| UART   | 设备       | 端口          |
| ------ | ---------- | ------------- |
| USART1 | /dev/ttyS0 | GPS1          |
| USART2 | /dev/ttyS1 | TELEM3        |
| USART3 | /dev/ttyS2 | Debug Console |
| UART5  | /dev/ttyS3 | TELEM2        |
| USART6 | /dev/ttyS4 | PX4IO         |
| UART7  | /dev/ttyS5 | TELEM1        |
| UART8  | /dev/ttyS6 | GPS2          |

## 尺寸

- [Pix32v6 尺寸](https://docs.holybro.com/autopilot/pix32-v6/dimensions)

## 电压额定值

如果提供三个电源，_Pix32 v6_ 可以在电源供应上实现三重冗余。三个电源轨是：**USB**、**POWER1**、**POWER2**（在 Pix32 v6 Mini-基板上不可用）。

**正常操作最大额定值**

在这些条件下，所有电源将按此顺序用于为系统供电：

1. **POWER1** 和 **POWER2** 输入（4.9V 至 5.5V）
1. **USB** 输入（4.75V 至 5.25V）

**绝对最大额定值**

在这些条件下，系统不会汲取任何电力（不会运行），但会保持完整。

1. **POWER1** 和 **POWER2** 输入（工作范围 4.1V 至 5.7V，0V 至 10V 不损坏）
1. **USB** 输入（工作范围 4.1V 至 5.7V，0V 至 6V 不损坏）
1. 舵机输入：**FMU PWM OUT** 和 **I/O PWM OUT** 的 VDD_SERVO 引脚（0V 至 42V 不损坏）

**电压监控**

Pix32 v6 使用模拟电源模块。

Holybro 为不同需求制造各种模拟[电源模块](../power_module/index.md)。

- [PM02 电源模块](../power_module/holybro_pm02.md)
- [PM06 电源模块](../power_module/holybro_pm06_pixhawk4mini_power_module.md)
- [PM07 电源模块](../power_module/holybro_pm07_pixhawk4_power_module.md)

## 构建固件

:::tip
大多数用户不需要构建此固件！
当连接适当的硬件时，它会由 _QGroundControl_ 预构建并自动安装。
:::

要为此目标[构建 PX4](../dev_setup/building_px4.md)：

```
make px4_fmu-v6c_default
```

<a id="debug_port"></a>

## 调试端口

[PX4 系统控制台](../debug/system_console.md) 和 [SWD 接口](../debug/swd_debug.md) 在 **FMU Debug** 端口上运行。

引脚分布和连接器符合 [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf) 接口中定义的 [Pixhawk Debug Full](../debug/swd_debug.md#pixhawk-debug-full) 接口（JST SM10B 连接器）。

| 引脚     | 信号             | 电压  |
| -------- | ---------------- | ----- |
| 1 (红)   | `Vtref`          | +3.3V |
| 2 (黑)   | Console TX (OUT) | +3.3V |
| 3 (黑)   | Console RX (IN)  | +3.3V |
| 4 (黑)   | `SWDIO`          | +3.3V |
| 5 (黑)   | `SWCLK`          | +3.3V |
| 6 (黑)   | `SWO`            | +3.3V |
| 7 (黑)   | NFC GPIO         | +3.3V |
| 8 (黑)   | PH11             | +3.3V |
| 9 (黑)   | nRST             | +3.3V |
| 10 (黑)  | `GND`            | GND   |

有关使用此端口的信息，请参见：

- [SWD 调试端口](../debug/swd_debug.md)
- [PX4 系统控制台](../debug/system_console.md)（注意，FMU 控制台映射到 USART3）。

## 外设

- [数字空速传感器](https://holybro.com/products/digital-air-speed-sensor-ms4525do)
- [遥测无线电模块](https://holybro.com/collections/telemetry-radios?orderby=date)
- [测距仪/距离传感器](../sensor/rangefinders.md)

## 支持的平台/机架

任何可以用普通 RC 舵机或 Futaba S-Bus 舵机控制的多旋翼/飞机/漫游车或船只。
完整的支持配置集可以在[机架参考](../airframes/airframe_reference.md)中看到。

## 更多信息

- [Holybro 文档](https://docs.holybro.com/)（Holybro）
- [参考：Pixhawk 6C 接线快速入门](../assembly/quick_start_pixhawk6c.md)
- [PM02 电源模块](../power_module/holybro_pm02.md)
- [PM06 电源模块](../power_module/holybro_pm06_pixhawk4mini_power_module.md)
- [PM07 电源模块](../power_module/holybro_pm07_pixhawk4_power_module.md)
- [FMUv6C 参考设计引脚分布](https://docs.google.com/spreadsheets/d/1FcmWRKd6zjdz3-cnjEDYEmANKZOFzNSc/edit?usp=sharing&ouid=113251442407318461574&rtpof=true&sd=true)。
- [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。
