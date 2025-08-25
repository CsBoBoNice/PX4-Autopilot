# CubePilot Cube Orange 飞行控制器

:::warning
PX4 不生产此（或任何）自驾仪。
如有硬件支持或合规性问题，请联系[制造商](https://cubepilot.org/#/home)。
:::

[Cube Orange](https://www.cubepilot.com/#/cube/features) 飞行控制器是一款灵活的自驾仪，主要面向商业系统制造商。

![Cube Orange](../../assets/flight_controller/cube/orange/cube_orange_hero.jpg)

该控制器设计为与特定领域的载板一起使用，以减少接线、提高可靠性并简化组装。
例如，商业检查飞行器的载板可能包括伴随计算机的连接，而竞速飞行器的载板可能包括适用于飞行器机架的电调。

ADS-B 载板包括来自 uAvionix 的定制 1090MHz ADSB-In 接收器。
这提供了 Cube 范围内商业载人飞机的姿态和位置信息。
这在默认 PX4 固件中自动配置和启用。

Cube 在其中两个 IMU 上包含减振，第三个固定 IMU 作为参考/备份。

:::tip
制造商的 [Cube 用户指南](https://docs.cubepilot.org/user-guides/autopilot/the-cube) 包含详细信息，包括 [Cube 颜色之间差异](https://docs.cubepilot.org/user-guides/autopilot/the-cube/introduction/specifications) 的概述。
:::

## 主要特点

- 32位 STM32H753VI（32位 [ARM Cortex M7](https://en.wikipedia.org/wiki/ARM_Cortex-M#Cortex-M7)，400 MHz，Flash 2MB，RAM 1MB）。
- 32 位 STM32F103 故障安全协处理器
- 14 个 PWM / 舵机输出（8 个带故障安全和手动覆盖，6 个辅助，高功率兼容）
- 丰富的连接选项用于额外外设（UART、I2C、CAN）
- 集成备份系统，用于飞行中恢复和手动覆盖，具有专用处理器和独立电源（固定翼使用）
- 备份系统集成混合功能，提供一致的自驾仪和手动覆盖混合模式（固定翼使用）
- 冗余电源输入和自动故障转移
- 外部安全开关
- 多色 LED 主要视觉指示器
- 高功率、多音调压电音频指示器
- microSD 卡用于长时间高速日志记录

<a id="stores"></a>

## 购买地点

- [经销商列表](https://www.cubepilot.com/#/reseller/list)

## 组装

[Cube 接线快速入门](../assembly/quick_start_cube.md)

## 规格

- **处理器：**
  - STM32H753VI（32位 [ARM Cortex M7](https://en.wikipedia.org/wiki/ARM_Cortex-M#Cortex-M7)）
  - 400 MHz
  - 1 MB RAM
  - 2 MB Flash（完全可访问）
- **故障安全协处理器：** <!-- inconsistent info on failsafe processor: 32 bit STM32F103 failsafe co-processor -->
  - STM32F103（32位 _ARM Cortex-M3_）
  - 24 MHz
  - 8 KB SRAM
- **传感器：**（均通过 SPI 连接）
  - **加速度计：**（3） ICM20948、ICM20649、ICM20602
  - **陀螺仪：**（3） ICM20948、ICM20649、ICM20602
  - **指南针：**（1） ICM20948
  - **气压传感器：**（2） MS5611
- **工作条件：**
  - **工作温度：** -10C 至 55C
  - **IP 等级/防水：** 不防水
  - **舵机导轨输入电压：** 3.3V / 5V
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
  - 5x UART（串行端口），1 个高功率兼容，2x 带硬件流量控制
  - 2x CAN（1 个带内部 3.3V 收发器，1 个在扩展连接器上）
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

### 顶部（GPS、TELEM 等）

![Cube Ports - Top (GPS, TELEM etc) and Main/AUX](../../assets/flight_controller/cube/cube_ports_top_main.jpg)

## 引脚分布

#### TELEM1、TELEM2 端口

| 引脚      | 信号      | 电压  |
| --------- | --------- | ----- |
| 1 (红色)  | VCC       | +5V   |
| 2 (黑色)  | TX (OUT)  | +3.3V |
| 3 (黑色)  | RX (IN)   | +3.3V |
| 4 (黑色)  | CTS (IN)  | +3.3V |
| 5 (黑色)  | RTS (OUT) | +3.3V |
| 6 (黑色)  | GND       | GND   |

#### GPS1 端口

| 引脚      | 信号          | 电压  |
| --------- | ------------- | ----- |
| 1 (红色)  | VCC           | +5V   |
| 2 (黑色)  | TX (OUT)      | +3.3V |
| 3 (黑色)  | RX (IN)       | +3.3V |
| 4 (黑色)  | SCL I2C2      | +3.3V |
| 5 (黑色)  | SDA I2C2      | +3.3V |
| 6 (黑色)  | Safety Button | GND   |
| 7 (黑色)  | Button LED    | GND   |
| 8 (黑色)  | GND           | GND   |

#### GPS2 端口

| 引脚      | 信号     | 电压  |
| --------- | -------- | ----- |
| 1 (红色)  | VCC      | +5V   |
| 2 (黑色)  | TX (OUT) | +3.3V |
| 3 (黑色)  | RX (IN)  | +3.3V |
| 4 (黑色)  | SCL I2C1 | +3.3V |
| 5 (黑色)  | SDA I2C1 | +3.3V |
| 6 (黑色)  | GND      | GND   |

#### ADC

| 引脚      | 信号   | 电压        |
| --------- | ------ | ----------- |
| 1 (红色)  | VCC    | +5V         |
| 2 (黑色)  | ADC IN | 最高 +6.6V |
| 3 (黑色)  | GND    | GND         |

#### I2C

| 引脚      | 信号 | 电压           |
| --------- | ---- | -------------- |
| 1 (红色)  | VCC  | +5V            |
| 2 (黑色)  | SCL  | +3.3 (pullups) |
| 3 (黑色)  | SDA  | +3.3 (pullups) |
| 4 (黑色)  | GND  | GND            |

#### CAN1 和 CAN2

| 引脚      | 信号  | 电压 |
| --------- | ----- | ---- |
| 1 (红色)  | VCC   | +5V  |
| 2 (黑色)  | CAN_H | +12V |
| 3 (黑色)  | CAN_L | +12V |
| 4 (黑色)  | GND   | GND  |

#### POWER1 和 POWER2

| 引脚      | 信号            | 电压  |
| --------- | --------------- | ----- |
| 1 (红色)  | VCC             | +5V   |
| 2 (红色)  | VCC             | +5V   |
| 3 (黑色)  | CURRENT sensing | +3.3V |
| 4 (黑色)  | VOLTAGE sensing | +3.3V |
| 5 (黑色)  | GND             | GND   |
| 6 (黑色)  | GND             | GND   |

#### USB

| 引脚      | 信号          | 电压     |
| --------- | ------------- | -------- |
| 1 (红色)  | VCC           | +5V      |
| 2 (黑色)  | OTG_DP1       | +3.3V    |
| 3 (黑色)  | OTG_DM1       | +3.3V    |
| 4 (黑色)  | GND           | GND      |
| 5 (黑色)  | BUZZER        | 电池电压 |
| 6 (黑色)  | FMU Error LED |

#### SPKT

| 引脚      | 信号 | 电压  |
| --------- | ---- | ----- |
| 1 (黑色)  | IN   |
| 2 (黑色)  | GND  | GND   |
| 3 (红色)  | OUT  | +3.3V |

#### TELEM1、TELEM2

| 引脚      | 信号      | 电压        |
| --------- | --------- | ----------- |
| 1 (红色)  | VCC       | +5V         |
| 2 (黑色)  | TX (OUT)  | +3.3V 至 5V |
| 3 (黑色)  | RX (IN)   | +3.3V 至 5V |
| 4 (黑色)  | CTS (OUT) | +3.3V 至 5V |
| 5 (黑色)  | RTS (IN)  | +3.3V 至 5V |
| 6 (黑色)  | GND       | GND         |

## 串行端口映射

| UART   | 设备       | 端口                  |
| ------ | ---------- | --------------------- |
| USART2 | /dev/ttyS0 | TELEM1（流量控制）    |
| USART3 | /dev/ttyS1 | TELEM2（流量控制）    |
| UART4  | /dev/ttyS2 | GPS1                  |
| USART6 | /dev/ttyS3 | PX4IO                 |
| UART7  | /dev/ttyS4 | CONSOLE/ADSB-IN       |
| UART8  | /dev/ttyS5 | GPS2                  |

### USB/SD卡端口

![Cube USB/SDCard Ports](../../assets/flight_controller/cube/cube_ports_usb_sdcard.jpg)

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，_QGroundControl_ 会自动安装。
:::

要为此目标[构建 PX4](../dev_setup/building_px4.md)，打开终端并输入：

```
make cubepilot_cubeorange
```

## 原理图

板卡原理图和其他文档可以在这里找到：[The Cube Project](https://github.com/proficnc/The-Cube)。

## 更多信息/文档

- [Cube 接线快速入门](../assembly/quick_start_cube.md)
- Cube 文档（制造商）：
  - [Cube 用户指南](https://docs.cubepilot.org/user-guides/autopilot/the-cube)
  - [Mini 载板](https://docs.cubepilot.org/user-guides/carrier-boards/mini-carrier-board)
