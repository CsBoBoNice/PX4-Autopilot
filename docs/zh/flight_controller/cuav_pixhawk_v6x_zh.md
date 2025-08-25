# CUAV Pixhawk V6X

:::warning
PX4 不制造此（或任何）自驾仪。
如需硬件支持或合规问题，请联系[制造商](https://store.cuav.net/)。
:::

_Pixhawk V6X_<sup>&reg;</sup> 是与 CUAV<sup>&reg;</sup> 和 PX4 团队合作设计和制造的 Pixhawk® 飞行控制器成功系列的最新更新版本。

它基于 [Pixhawk​​® Autopilot FMUv6X Standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-012%20Pixhawk%20Autopilot%20v6X%20Standard.pdf)、[Autopilot Bus Standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf) 和 [Connector Standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。

![Pixhawk V6X](../../assets/flight_controller/cuav_pixhawk_v6x/pixhawk_v6x.jpg)

:::tip
此自驾仪由 PX4 维护和测试团队[支持](../flight_controller/autopilot_pixhawk_standard.md)。
:::

Pixhawk<sup>&reg;</sup> V6X 在各个方面为您带来极致的性能、稳定性和可靠性。

- Arm® Cortex®-M7 处理器 (STM32H753) 带浮点单元 (FPU)，480MHz 高速运算和 2MB 闪存。
  开发人员可以提高生产力和效率，允许更复杂的算法和模型。
- 基于 FMUv6X 开放标准的高性能板载低噪声 IMU 和汽车级磁力计。
  旨在实现更好的稳定性和抗干扰能力。
- 三重冗余 IMU 和双重冗余气压计分布在独立总线上。
  当 PX4 自驾仪检测到传感器故障时，系统会无缝切换到另一个传感器以保持飞行控制可靠性。
- 独立的 LDO 为每个传感器组供电，具有独立的电源控制。
  振动隔离系统过滤高频振动并降低噪声以确保准确读数，使飞行器达到更好的整体飞行性能。
- 外部传感器总线 (SPI5) 有两条片选线和数据就绪信号，适用于具有 SPI 接口的额外传感器和载荷。
- 集成 Microchip 以太网 PHY，通过以太网与机载设备（如任务计算机）进行高速通信。
- 新设计的振动隔离系统，过滤高频振动并降低噪声以确保准确读数。
- IMU 由板载加热电阻器进行温度控制，允许 IMU 的最佳工作温度。
- 模块化飞行控制器：独立的 IMU、FMU 和基础系统通过 100 引脚和 50 引脚 Pixhawk®​ 自驾仪总线连接器连接。

Pixhawk® V6X 是企业研究实验室、学术研究和商业应用的理想选择。

### 处理器和传感器

- FMU 处理器：STM32H753
  - 32 位 Arm® Cortex®-M7，480MHz，2MB 闪存，1MB RAM
- IO 处理器：STM32F103
  - 32 位 Arm® Cortex®-M3，72MHz，20KB SRAM
- 板载传感器
  - 加速度计/陀螺仪：BMI088
  - 加速度计/陀螺仪：ICM-42688-P
  - 加速度计/陀螺仪：ICM-20649
  - 磁力计：RM3100
  - 气压计：2x ICP-20100

### 电气数据

- 电压额定值：
  - 最大输入电压：5.7V
  - USB 电源输入：4.75\~5.25V
  - 舵机轨输入：0\~9.9V
- 电流额定值：
  - TELEM1 和 GPS2 组合输出电流限制器：1.5A
  - 所有其他端口组合输出电流限制器：1.5A

### 接口

- 16 个 PWM 舵机输出
- 1 个专用 R/C 输入，用于 Spektrum / DSM 和 S.Bus，带模拟 / PWM RSSI 输入
- 3 个 TELEM 端口（具有完整流量控制）
- 1 个 UART4（串行和 I2C）
- 2 个 GPS 端口
  - 1 个完整 GPS 加安全开关端口（GPS1）
  - 1 个基本 GPS 端口（带 I2C，GPS2）
- 2 个 USB 端口
  - 1 个 TYPE-C
  - JST GH1.25
- 1 个以太网端口
  - 无变压器应用
  - 100Mbps
- 1 个 SPI 总线
  - 2 条片选线
  - 2 条数据就绪线
  - 1 条 SPI 同步线
  - 1 条 SPI 复位线
- 2 个用于 CAN 外设的 CAN 总线
  - CAN 总线具有独立的静默控制或 ESC RX-MUX 控制
- 4 个电源输入端口
  - 2 个 Dronecan/UAVCAN 电源输入
  - 2 个 SMBUS/I2C 电源输入
- 1 个 AD 和 IO 端口
  - 2 个额外的模拟输入（3.3 和 6.6v）
  - 1 个 PWM/捕获输入
- 2 个专用调试
  - FMU 调试
  - IO 调试

### 机械数据

- 重量
  - 飞行控制器模块：99g
  - 核心模块：43g
  - 基板：56g
- 工作和存储温度：-20 ~ 85°c
- 尺寸
  - 飞行控制器

    ![Pixhawk V6X](../../assets/flight_controller/cuav_pixhawk_v6x/v6x_size.jpg)

  - 核心模块

    ![Pixhawk V6X](../../assets/flight_controller/cuav_pixhawk_v6x/core.png)

## 购买渠道

从 [CUAV](https://store.cuav.net/) 订购。

## 组装/设置

[Pixhawk V6X 接线快速入门](../assembly/quick_start_cuav_pixhawk_v6x.md) 提供了如何组装必需/重要外设（包括 GPS、电源模块等）的说明。

## 引脚分布

![Pixhawk V6x 引脚分布](../../assets/flight_controller/cuav_pixhawk_v6x/pixhawk_v6x_pinouts.png)

注意：

- [相机捕获引脚](../camera/fc_connected_camera.md#camera-capture-configuration) (`PI0`) 是 AD&IO 端口上的引脚 2，上面标记为 `FMU_CAP1`。

## 串口映射

| UART   | 设备       | 端口          |
| ------ | ---------- | ------------- |
| USART1 | /dev/ttyS0 | GPS           |
| USART2 | /dev/ttyS1 | TELEM3        |
| USART3 | /dev/ttyS2 | Debug Console |
| UART4  | /dev/ttyS3 | UART4         |
| UART5  | /dev/ttyS4 | TELEM2        |
| USART6 | /dev/ttyS5 | PX4IO/RC      |
| UART7  | /dev/ttyS6 | TELEM1        |
| UART8  | /dev/ttyS7 | GPS2          |

## 电压额定值

如果提供三个电源，_Pixhawk V6X_ 可以在电源供应上实现三重冗余。
这三个电源轨是：**POWERC1/POWER1**、**POWERC2/POWER2** 和 **USB**。

- **POWER C1** 和 **POWER C2** 是 DroneCAN/UAVCAN 电池接口（推荐）；**POWER1** 和 **POWER2** 是 SMbus/I2C 电池接口（备用）。
- **POWER C1** 和 **POWER1** 使用相同的电源开关，**POWER C2** 和 **POWER2** 使用相同的电源开关。

**正常操作最大额定值**

在这些条件下，所有电源将按此顺序用于为系统供电：

1. **POWER C1**、**POWER C2**、**POWER1** 和 **POWER2** 输入（4.75V 至 5.7V）
2. **USB** 输入（4.75V 至 5.25V）

**绝对最大额定值**

在这些条件下，系统不会汲取任何电力（不会运行），但会保持完整。

1. **POWER1** 和 **POWER2** 输入（工作范围 4.7V 至 5.7V，0V 至 10V 不损坏）
1. **USB 输入**（工作范围 4.7V 至 5.7V，0V 至 6V 不损坏）
1. **舵机输入：** **FMU PWM OUT** 和 **I/O PWM OUT** 的 `VDD_SERVO` 引脚（0V 至 42V 不损坏）

**电压监控**

默认情况下启用数字 DroneCAN/UAVCAN 电池监控（参见 [快速入门 > 电源](../assembly/quick_start_cuav_pixhawk_v6x.md#power)）。

::: info
此特定板不支持通过 ADC 进行模拟电池监控，但在具有不同基板的此飞行控制器的变体中可能受支持。
:::

## 构建固件

:::tip
大多数用户不需要构建此固件！
当连接适当的硬件时，它会由 _QGroundControl_ 预构建并自动安装。
:::

要为此目标[构建 PX4](../dev_setup/building_px4.md)：

```
make px4_fmu-v6x_default
```

<a id="debug_port"></a>

## 调试端口

[PX4 系统控制台](../debug/system_console.md) 和 [SWD 接口](../debug/swd_debug.md) 在 **FMU Debug** 端口上运行。

引脚分布和连接器符合 [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf) 接口中定义的 [Pixhawk Debug Full](../debug/swd_debug.md#pixhawk-debug-full) 接口（JST SM10B 连接器）。

| 引脚      | 信号             | 电压  |
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

有关接线和使用此端口的信息，请参见：

- [PX4 系统控制台](../debug/system_console.md#pixhawk_debug_port)（注意，FMU 控制台映射到 USART3）。
- [SWD 调试端口](../debug/swd_debug.md)

## 外设

- [数字空速传感器](https://holybro.com/products/digital-air-speed-sensor-ms4525do)
- [遥测无线电模块](https://holybro.com/collections/telemetry-radios?orderby=date)
- [测距仪/距离传感器](../sensor/rangefinders.md)

## 支持的平台/机架

任何可以用普通 RC 舵机或 Futaba S-Bus 舵机控制的多旋翼/飞机/漫游车或船只。
完整的支持配置集可以在[机架参考](../airframes/airframe_reference.md)中看到。

## 更多信息

- [CUAV 文档](https://doc.cuav.net/)（CUAV）
- [Pixhawk V6X 接线快速入门](../assembly/quick_start_cuav_pixhawk_v6x.md)
- [Pixhawk Autopilot FMUv6X 标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-012%20Pixhawk%20Autopilot%20v6X%20Standard.pdf)
- [Pixhawk Autopilot Bus 标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf)
- [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)
