# Holybro Pixhawk 6X Pro

:::warning
PX4 不制造此产品（或任何其他自动驾驶仪）。
如有硬件支持或合规问题，请联系[制造商](https://holybro.com/)。
:::

![Pixhawk6X Pro 内部架构](../../assets/flight_controller/pixhawk6x_pro/pixhawk6x_pro_internal_architecture.jpeg)

## 主要设计要点

- 高性能 ADIS16470 工业级 IMU，具有高加速度计动态范围（±40 g），非常适合在苛刻的无人机应用中进行精确运动感测
- 全新先进耐用振动隔离材料，在高频谱中具有共振频率，非常适合工业和商用无人机应用
- 高性能 STM32H753 处理器
- 用于高速任务计算机集成的以太网接口

## 基板

Pixhawk 6X Pro 可以购买多种基板（或无基板）以适应不同的使用案例和车辆类型，包括 [Standard v2A](https://docs.holybro.com/autopilot/pixhawk-baseboards/pixhawk-baseboard-v2-ports)、[Standard v2B](https://docs.holybro.com/autopilot/pixhawk-baseboards/pixhawk-baseboard-v2-ports) 和 [Mini](https://docs.holybro.com/autopilot/pixhawk-baseboards/pixhawk-mini-baseboard-ports)，如下所示。
它也可以与任何其他符合 Pixhawk 自动驾驶仪总线（PAB）规范的基板一起使用，例如 [Holybro Pixhawk Jetson 基板](../companion_computer/holybro_pixhawk_jetson_baseboard.md) 和 [Holybro Pixhawk RPi CM4 基板](../companion_computer/holybro_pixhawk_rpi_cm4_baseboard.md)。

:::: tabs

::: tab Pixhawk 6X Pro Standard v2A

![Pixhawk 6X Pro Standard v2A](../../assets/flight_controller/pixhawk6x_pro/pixhawk6x_pro_v2a.webp)

:::

::: tab Pixhawk 6X Pro Standard v2B

![Pixhawk 6X Pro Standard v2B](../../assets/flight_controller/pixhawk6x_pro/pixhawk6x_pro_v2b.webp)
:::

::: tab Pixhawk 6X Pro Mini

![Pixhawk 6X Pro Mini](../../assets/flight_controller/pixhawk6x_pro/pixhawk6x_pro_mini.webp)
:::

::::

## 特性

- 在独立总线上三重冗余 IMU 和双重冗余气压计
- 模块化飞行控制器：独立的 IMU、FMU 和基础系统
- 安全驱动设计，集成了来自不同制造商和型号系列的传感器
- 独立 LDO 为每个传感器组供电，具有独立的电源控制。
- 温控 IMU 板，使 IMU 达到最佳工作温度

::: details 处理器和传感器

- FMU 处理器：STM32H753
  - 32位 Arm® Cortex®-M7，480MHz，2MB 闪存，1MB RAM
- IO 处理器：STM32F103
  - 32位 Arm® Cortex®-M3，72MHz，64KB SRAM
- 板载传感器
  - 加速度计/陀螺仪：ADIS16470（±40g，振动隔离，工业级 IMU）
  - 加速度计/陀螺仪：IIM-42652（±16g，振动隔离，工业级 IMU）
  - 加速度计/陀螺仪：ICM-45686 带 BalancedGyro™ 技术（±32g，硬安装）
  - 气压计：ICP20100
  - 气压计：BMP388
  - 磁力计：BMM150

:::

::: details 电气数据

- 电压额定值：
  - 最大输入电压：6V
  - USB 电源输入：4.75~5.25V
  - 舵机导轨输入：0~36V
- 电流额定值：
  - Telem1 输出电流限制器：1.5A
  - 所有其他端口组合输出电流限制器：1.5A

:::

::: details 机械数据

- 尺寸
  - 飞行控制器模块：38.8 x 31.8 x 30.1mm
  - 标准基板：52.4 x 103.4 x 16.7mm
  - Mini 基板：43.4 x 72.8 x 14.2 mm
- 重量
  - 飞行控制器模块：50g
  - 标准基板：51g
  - Mini 基板：26.5g

:::

::: details 接口

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

:::

## 购买地点

从 [Holybro](https://holybro.com/products/pixhawk-6x-pro) 订购。

## 组装/设置

[Pixhawk 6X 接线快速入门](../assembly/quick_start_pixhawk6x.md) 提供了如何组装所需/重要外设（包括 GPS、电源模块等）的说明。

## 连接

### 多旋翼接线示例

![Pixhawk 6X Pro 接线概览](../../assets/flight_controller/pixhawk6x_pro/pixhawk6x_pro_wiring_diagram.png)

### VTOL 接线示例

![Pixhawk 6X Pro VTOL 固定翼接线概览](../../assets/flight_controller/pixhawk6x_pro/pixhawk6x_pro_wiring_diagram_vtol.webp)

## 引脚图

- [Holybro Pixhawk 基板引脚图](https://docs.holybro.com/autopilot/pixhawk-6x/pixhawk-baseboard-pinout)
- [Holybro Pixhawk Mini 基板引脚图](https://docs.holybro.com/autopilot/pixhawk-6x/pixhawk-mini-baseboard-pinout)
- [Holybro Pixhawk Jetson 基板](https://docs.holybro.com/autopilot/pixhawk-baseboards/pixhawk-jetson-baseboard)
- [Holybro Pixhawk RPi CM4 基板](https://docs.holybro.com/autopilot/pixhawk-baseboards/pixhawk-rpi-cm4-baseboard)

注意：

- [相机捕获引脚](../camera/fc_connected_camera.md#camera-capture-configuration)（`PI0`）是 AD&IO 端口上的引脚 2，标记为 `FMU_CAP1`。

## 串口映射

| UART   | Device     | Port          |
| ------ | ---------- | ------------- |
| USART1 | /dev/ttyS0 | GPS           |
| USART2 | /dev/ttyS1 | TELEM3        |
| USART3 | /dev/ttyS2 | 调试控制台     |
| UART4  | /dev/ttyS3 | UART4 & I2C   |
| UART5  | /dev/ttyS4 | TELEM2        |
| USART6 | /dev/ttyS5 | PX4IO/RC      |
| UART7  | /dev/ttyS6 | TELEM1        |
| UART8  | /dev/ttyS7 | GPS2          |

## 尺寸

[Pixhawk 6X Pro 尺寸](https://docs.holybro.com/autopilot/pixhawk-6x-pro/dimensions)

## 电压额定值

如果提供三个电源，_Pixhawk 6X Pro_ 可以在电源上实现三重冗余。
三个电源导轨是：**POWER1**、**POWER2** 和 **USB**。
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
make px4_fmu-v6x_default
```

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

- [遥测无线电模块](https://holybro.com/collections/telemetry-radios?orderby=date)
- [测距仪/距离传感器](../sensor/rangefinders.md)
- [Holybro 传感器](https://holybro.com/collections/sensors)
- [Holybro GPS & RTK 系统](https://holybro.com/collections/gps-rtk-systems)
- [电源模块 & PDB](https://holybro.com/collections/power-modules-pdbs)

## 支持的平台/机架

任何可以用普通 RC 舵机或 Futaba S-Bus 舵机控制的多旋翼/飞机/地面车辆或船舶。
完整的支持配置集合可以在[机架参考](../airframes/airframe_reference.md)中看到。

## CAD 文件

[在此处](https://docs.holybro.com/autopilot/pixhawk-6x-pro/download)下载。

## 另请参阅

- [Holybro 文档](https://docs.holybro.com/autopilot/pixhawk-6x-pro)（Holybro）
- [Pixhawk 6X 接线快速入门](../assembly/quick_start_pixhawk6x.md)
- [Pixhawk 自动驾驶仪 FMUv6X 标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-012%20Pixhawk%20Autopilot%20v6X%20Standard.pdf)。
- [Pixhawk 自动驾驶仪总线标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf)。
- [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。
