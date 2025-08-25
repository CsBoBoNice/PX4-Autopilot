# CubePilot Cube Orange+ 飞行控制器

:::warning
PX4 不制造此（或任何）自驾仪。
如需硬件支持或合规问题，请联系[制造商](https://cubepilot.org/#/home)。
:::

[Cube Orange+](https://www.cubepilot.com/#/cube/features) 飞行控制器是一个灵活的自驾仪，主要面向商业系统制造商。
Cube Orange+ 类似于 Cube Orange，但具有更强大的双核处理器（STM32H757），以及一些不同的传感器部件。

![Cube Orange](../../assets/flight_controller/cube/orangeplus/cubepilot_cube_orangeplus_standard_set.jpg)

该控制器设计为与特定领域的载板一起使用，以减少接线、提高可靠性并简化组装。
例如，商业检查飞行器的载板可能包括配套计算机的连接，而竞速飞行器的载板可能包括飞行器框架的 ESC。

ADS-B 载板包括来自 uAvionix 的定制 1090MHz ADSB-In 接收器。
这提供了 Cube 范围内商业载人飞机的姿态和位置。
这在默认 PX4 固件中自动配置和启用。

Cube 在两个 IMU 上包括振动隔离，第三个固定 IMU 作为参考/备份。

:::tip
制造商的 [Cube 用户指南](https://docs.cubepilot.org/user-guides/autopilot/the-cube) 包含详细信息，包括 [Cube 颜色之间差异](https://docs.cubepilot.org/user-guides/autopilot/the-cube/introduction/specifications) 的概述。
:::

## 主要特性

- 32 位 STM32H757ZI（32 位 [ARM Cortex M7](https://en.wikipedia.org/wiki/ARM_Cortex-M#Cortex-M7)，400 MHz，闪存 2MB，RAM 1MB）。
- 32 位 STM32F103 故障安全协处理器
- 14 个 PWM / 舵机输出（8 个具有故障安全和手动覆盖，6 个辅助，高功率兼容）
- 丰富的附加外设连接选项（UART、I2C、CAN）
- 集成备份系统，用于飞行中恢复和手动覆盖，具有专用处理器和独立电源（固定翼使用）
- 备份系统集成混控，提供一致的自驾仪和手动覆盖混控模式（固定翼使用）
- 冗余电源输入和自动故障切换
- 外部安全开关
- 多色 LED 主视觉指示器
- 高功率、多音调压电音频指示器
- microSD 卡，用于长时间高速率记录

<a id="stores"></a>

## 购买渠道

- [经销商列表](https://www.cubepilot.com/#/reseller/list)

## 组装

[Cube 接线快速入门](../assembly/quick_start_cube.md)

## 规格

- **处理器：**
  - STM32H757（32 位 [ARM Cortex M7](https://en.wikipedia.org/wiki/ARM_Cortex-M#Cortex-M7)）
  - 400 MHz
  - 1 MB RAM
  - 2 MB 闪存（完全可访问）
- **故障安全协处理器：** <!-- 故障安全处理器信息不一致：32 位 STM32F103 故障安全协处理器 -->
  - STM32F103（32 位 _ARM Cortex-M3_）
  - 24 MHz
  - 8 KB SRAM
- **传感器：**（全部通过 SPI 连接）
  - **加速度计：**（3）ICM42688p、ICM20948、ICM20649
  - **陀螺仪：**（3）ICM42688p、ICM20948、ICM20649
  - **指南针：**（1）ICM20948
  - **气压传感器：**（2）MS5611
- **工作条件：**
  - **工作温度：** -10°C 至 55°C
  - **IP 等级/防水：** 不防水
  - **舵机轨输入电压：** 3.3V / 5V
  - **USB 端口输入：**
    - 电压：4V - 5.7V
    - 额定电流：250 mA
  - **电源：**
    - 输入电压：4.1V - 5.7V
    - 额定输入电流：2.5A
    - 额定输入/输出功率：14W
- **尺寸：**
  - **Cube：** 38.25mm x 38.25mm x 22.3mm
  - **载板：** 94.5mm x 44.3mm x 17.3mm
- **接口**
  - IO 端口：14 个 PWM 舵机输出（8 个来自 IO，6 个来自 FMU）
  - 5x UART（串行端口），一个高功率能力，2x 具有硬件流量控制
  - 2x CAN（一个具有内部 3.3V 收发器，一个在扩展连接器上）
  - **R/C 输入：**
    - Spektrum DSM / DSM2 / DSM-X® 卫星兼容输入
    - Futaba S.BUS® 兼容输入和输出
    - PPM-SUM 信号输入
  - RSSI（PWM 或电压）输入
  - I2C
  - SPI
  - 3.3v ADC 输入
  - 内部 microUSB 端口和外部 microUSB 端口扩展

## 端口

### 顶侧（GPS、TELEM 等）

![Cube 端口 - 顶部（GPS、TELEM 等）和 Main/AUX](../../assets/flight_controller/cube/cube_ports_top_main.jpg)

## 引脚分布

#### TELEM1、TELEM2 端口

| 引脚    | 信号      | 电压  |
| ------- | --------- | ----- |
| 1 (红)  | VCC       | +5V   |
| 2 (黑)  | TX (OUT)  | +3.3V |
| 3 (黑)  | RX (IN)   | +3.3V |
| 4 (黑)  | CTS (IN)  | +3.3V |
| 5 (黑)  | RTS (OUT) | +3.3V |
| 6 (黑)  | GND       | GND   |

#### GPS1 端口

| 引脚    | 信号          | 电压  |
| ------- | ------------- | ----- |
| 1 (红)  | VCC           | +5V   |
| 2 (黑)  | TX (OUT)      | +3.3V |
| 3 (黑)  | RX (IN)       | +3.3V |
| 4 (黑)  | SCL I2C2      | +3.3V |
| 5 (黑)  | SDA I2C2      | +3.3V |
| 6 (黑)  | Safety Button | GND   |
| 7 (黑)  | Button LED    | GND   |
| 8 (黑)  | GND           | GND   |

<!-- 检查是否为 i2c2 -->

#### GPS2 端口

| 引脚    | 信号     | 电压  |
| ------- | -------- | ----- |
| 1 (红)  | VCC      | +5V   |
| 2 (黑)  | TX (OUT) | +3.3V |
| 3 (黑)  | RX (IN)  | +3.3V |
| 4 (黑)  | SCL I2C1 | +3.3V |
| 5 (黑)  | SDA I2C1 | +3.3V |
| 6 (黑)  | GND      | GND   |

#### ADC

| 引脚    | 信号   | 电压        |
| ------- | ------ | ----------- |
| 1 (红)  | VCC    | +5V         |
| 2 (黑)  | ADC IN | 最高 +6.6V |
| 3 (黑)  | GND    | GND         |

#### I2C

| 引脚    | 信号 | 电压             |
| ------- | ---- | ---------------- |
| 1 (红)  | VCC  | +5V              |
| 2 (黑)  | SCL  | +3.3（上拉电阻） |
| 3 (黑)  | SDA  | +3.3（上拉电阻） |
| 4 (黑)  | GND  | GND              |

#### CAN1 和 CAN2

| 引脚    | 信号  | 电压 |
| ------- | ----- | ---- |
| 1 (红)  | VCC   | +5V  |
| 2 (黑)  | CAN_H | +12V |
| 3 (黑)  | CAN_L | +12V |
| 4 (黑)  | GND   | GND  |

#### POWER1 和 POWER2

| 引脚    | 信号            | 电压  |
| ------- | --------------- | ----- |
| 1 (红)  | VCC             | +5V   |
| 2 (红)  | VCC             | +5V   |
| 3 (黑)  | CURRENT sensing | +3.3V |
| 4 (黑)  | VOLTAGE sensing | +3.3V |
| 5 (黑)  | GND             | GND   |
| 6 (黑)  | GND             | GND   |

#### USB

| 引脚    | 信号          | 电压     |
| ------- | ------------- | -------- |
| 1 (红)  | VCC           | +5V      |
| 2 (黑)  | OTG_DP1       | +3.3V    |
| 3 (黑)  | OTG_DM1       | +3.3V    |
| 4 (黑)  | GND           | GND      |
| 5 (黑)  | BUZZER        | 电池电压 |
| 6 (黑)  | FMU Error LED |

#### SPKT

| 引脚    | 信号 | 电压  |
| ------- | ---- | ----- |
| 1 (黑)  | IN   |
| 2 (黑)  | GND  | GND   |
| 3 (红)  | OUT  | +3.3V |

#### TELEM1、TELEM2

| 引脚    | 信号      | 电压        |
| ------- | --------- | ----------- |
| 1 (红)  | VCC       | +5V         |
| 2 (黑)  | TX (OUT)  | +3.3V 至 5V |
| 3 (黑)  | RX (IN)   | +3.3V 至 5V |
| 4 (黑)  | CTS (OUT) | +3.3V 至 5V |
| 5 (黑)  | RTS (IN)  | +3.3V 至 5V |
| 6 (黑)  | GND       | GND         |

## 串口映射

| UART   | 设备       | 端口                  |
| ------ | ---------- | --------------------- |
| USART2 | /dev/ttyS0 | TELEM1（流量控制）    |
| USART3 | /dev/ttyS1 | TELEM2（流量控制）    |
| UART4  | /dev/ttyS2 | GPS1                  |
| USART6 | /dev/ttyS3 | PX4IO                 |
| UART7  | /dev/ttyS4 | CONSOLE/ADSB-IN       |
| UART8  | /dev/ttyS5 | GPS2                  |

<!-- 注意：使用 https://github.com/PX4/PX4-user_guide/pull/672#issuecomment-598198434 获取端口 -->
<!-- https://github.com/PX4/PX4-Autopilot/blob/main/boards/cubepilot/cubeorange/default.px4board -->
<!-- https://github.com/PX4/PX4-Autopilot/blob/main/boards/cubepilot/cubeorange/nuttx-config/nsh/defconfig#L188-L197 -->

### USB/SD 卡端口

![Cube USB/SD 卡端口](../../assets/flight_controller/cube/cube_ports_usb_sdcard.jpg)

## 构建固件

:::warning
Orange+ 的固件将在 PX4 v1.14 版本中提供。
:::

要为此目标[构建 PX4](../dev_setup/building_px4.md)，打开终端并输入：

```
make cubepilot_cubeorangeplus
```

::: info
Cube Orange+ 和 Cube Orange 的固件不兼容。
由于 STM32H757 的电源功能，它需要 [NuttX 中的更新](https://github.com/PX4/NuttX/pull/214)，因此需要新的板配置、引导加载程序、构建目标等。
:::

## 原理图

板原理图和其他文档可以在这里找到：[The Cube Project](https://github.com/proficnc/The-Cube)。

## 更多信息/文档

- [Cube 接线快速入门](../assembly/quick_start_cube.md)
- Cube 文档（制造商）：
  - [Cube 用户指南](https://docs.cubepilot.org/user-guides/autopilot/the-cube)
  - [Mini 载板](https://docs.cubepilot.org/user-guides/carrier-boards/mini-carrier-board)
