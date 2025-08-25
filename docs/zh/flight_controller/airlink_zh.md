# Sky-Drones AIRLink

:::warning
PX4 不生产此（或任何）自驾仪。
如有硬件支持或合规性问题，请联系[制造商](https://sky-drones.com/)。
:::

[AIRLink](https://sky-drones.com/airlink) 代表人工智能与远程链接（Artificial Intelligence & Remote Link）。该设备包含了尖端的无人机自驾仪、AI 任务计算机和 LTE/5G 连接单元。AIRLink 有助于将新无人机制造商的上市时间从数年或数月缩短到几周。

![AIRLink](../../assets/flight_controller/airlink/airlink-main.jpg)

::: info
此飞行控制器由[制造商支持](../flight_controller/autopilot_manufacturer_supported.md)。
:::

AIRLink 包含两台计算机和集成的 LTE 模块：

- 飞行控制计算机（自驾仪）具有三重冗余减振和温度稳定的 IMU。
- 强大的 AI 任务计算机支持先进的无人机软件功能，如计算机视觉和避障、数字高清视频流和载荷数据流。
- LTE/5G 和 WiFi 连接模块提供永久的宽带互联网连接，这是实现远程工作流程的关键。

## 特色亮点

<lite-youtube videoid="VcBx9DLPN54" title="SmartAP AIRLink - The Most Advanced AI Drone Avionics"/>

## 规格

- **传感器**

  - 3个加速度计、3个陀螺仪、3个磁力计、3个压力传感器
  - GNSS、测距仪、激光雷达、光流、摄像头
  - 3重冗余 IMU
  - 减振
  - 温度稳定

- **飞行控制器**

  - STM32F7，ARM Cortex M7 带 FPU，216 MHz，2MB Flash，512 kB RAM
  - STM32F1，I/O 协处理器
  - 以太网，10/100 Mbps
  - 与 AI 任务计算机的局域网
  - 8个 UART：遥测 1、遥测 2（AI 任务计算机）、遥测 3、GPS 1、GPS 2、额外 UART、串行调试控制台、IO
  - 2个 CAN：CAN1、CAN2
  - 带 MAVLink 的 USB
  - 用于调试的串行控制台
  - RC 输入、SBUS 输入、RSSI 输入、PPM 输入
  - 16个 PWM 舵机输出（8个来自 IO，8个来自 FMU）
  - 3个 I2C 端口
  - 高功率压电蜂鸣器驱动器
  - 高功率 RGB LED
  - 安全开关/LED 选项

- **AI 任务计算机**

  - 6核 CPU：双核 Cortex-A72 + 四核 Cortex-A53
  - GPU Mali-T864，OpenGL ES1.1/2.0/3.0/3.1
  - VPU 支持 4K VP8/9，4K 10位 H265/H264 60fps 解码
  - 远程电源控制、软件重置、关机、RTC 唤醒、睡眠模式
  - RAM 双通道 4GB LPDDR4
  - 16GB eMMC
  - MicroSD 最大 256GB
  - 以太网 10/100/1000 原生千兆位
  - WiFi 802.11a/b/g/n/ac，蓝牙
  - USB 3.0 Type C
  - 2个视频：4通道 MIPI CSI（FPV 摄像头）和 4通道 MIPI CSI 带 HDMI 输入（载荷摄像头）

- **LTE/5G 连接模块**

  - 最高 600 Mbps 带宽
  - 5G sub-6 和 mmWave，SA 和 NSA 操作
  - 4G Cat 20，最多 7xCA，256-QAM DL/UL，2xCA UL
  - 4G 和 5G（sub-6 频段）的 4 x 4 MIMO
  - 3G HSPA+
  - 通过 JRL/JTBL、FCC、PTCRB、RED、GCF 认证
  - 天线，4x4 MIMO
  - 频段：全球

## 购买地点

从原厂 Sky-Drones 商店购买（全球发货，1-2 天订单处理时间）：

- [购买 AIRLink Enterprise 4G](https://sky-drones.com/sets/airlink-enterprise-set.html)
- [购买 AIRLink Enterprise 5G](https://sky-drones.com/sets/airlink-5g-enterprise-set.html)
- [购买 AIRLink Core 4G](https://sky-drones.com/autopilots/airlink-core.html)
- [购买 AIRLink Core 5G](https://sky-drones.com/store/airlink-5g-core.html)

## AIRLink Enterprise 套件配件

<lite-youtube videoid="lex7axW8WQg" title="SmartAP AIRLink - Unboxing"/>

AIRLink Enterprise 包含设置自驾仪系统所需的一切。

标准套装包含：

- 1个 AIRLink Enterprise 单元
- 1个带 CSI 线缆的 FPV 摄像头
- 1个带 MMCX 连接器的 WiFi 天线
- 2个/4个带 MMCX 连接器的 LTE/5G 天线
- 1根 HDMI 到 mini HDMI 线缆
- 1套线缆（所有连接器的 7 根线缆）

基于 Microhard LAN/IP 的 RF 微模块的 [AIRLink 遥测](https://sky-drones.com/sets/airlink-telemetry-set.html) 可作为附加产品购买，完全兼容 AIRLink。

## 版本

AIRLink 有不同的版本，提供无人机制造商所需的不同集成级别：_Enterprise_ 和 _Core_。
AIRLink Enterprise 适合快速入门、评估和原型制作，而 Core 版本优化用于深度集成和中高批量制造。

**AIRLink Enterprise**

SmartAP AIRLink 的 Enterprise 版本适用于原型制作和中低批量无人机生产。
由于专用安装孔和集成散热器，安装快速简便，便于功率散热。

![AIRLink Enterprise](../../assets/flight_controller/airlink/airlink-enterprise.jpg)

**AIRLink Core**

SmartAP AIRLink 的 Core 版本适用于中高批量生产和与客户硬件的深度集成。重量仅为 89 克，可以安装在金属框架上以获得最佳冷却效果。

![AIRLink Core](../../assets/flight_controller/airlink/airlink-core.jpg)

| 参数        | AIRLink Enterprise                                      | AIRLink Core                                        |
| ----------- | ------------------------------------------------------- | --------------------------------------------------- |
| 外壳        | 铝制，带集成散热器和风扇安装选项。                      | 设计应提供外部散热器或合理的功率散热。              |
| 尺寸        | L103 x W61 x H37 mm                                     | L100 x W57 x H22 mm                                 |
| 重量        | 198 g                                                   | 89 g                                                |
| 环境温度    | -40°C..+50°C                                            | -40°C..+50°C                                        |

## 主要特点

- **易于安装**

  ![Easy mount](../../assets/flight_controller/airlink/airlink-easy-to-mount.jpg)

- **标配 FPV 摄像头**

  ![FPV camera comes as standard](../../assets/flight_controller/airlink/airlink-fpv-camera.jpg)

## 接口

### 左侧

![Left side](../../assets/flight_controller/airlink/airlink-interfaces-left.jpg)

- **左侧接口：**

  - 带电压和电流监控的电源输入
  - AI 任务计算机 micro SD 卡
  - 飞行控制器 micro SD 卡
  - AI 任务计算机 USB Type-C
  - PPM 输入、SBUS 输出、RSSI 监控

- **电源 - JST GH SM10B-GHS-TB**

  | 引脚编号 | 引脚名称    | 方向 | 电压  | 功能           |
  | -------- | ----------- | ---- | ----- | -------------- |
  | 1        | 12V         | IN   | +12V  | 主电源输入     |
  | 2        | 12V         | IN   | +12V  | 主电源输入     |
  | 3        | 12V         | IN   | +12V  | 主电源输入     |
  | 4        | BAT_CURRENT | IN   | +3.3V | 电池电流监控   |
  | 5        | BAT_VOLTAGE | IN   | +3.3V | 电池电压监控   |
  | 6        | 3V3         | OUT  | +3.3V | 3.3V 输出      |
  | 7        | PWR_KEY     | IN   | +3.3V | 电源键输入     |
  | 8        | GND         | 接地 |       |                |
  | 9        | GND         | 接地 |       |                |
  | 10       | GND         | 接地 |       |                |

- **CPU SD 卡 - microSD**
- **CPU USB - USB Type C**
- **RC 连接器 - JST GH SM06B-GHS-TB**

  | 引脚编号 | 引脚名称 | 方向 | 电压  | 功能      |
  | -------- | -------- | ---- | ----- | --------- |
  | 1        | 5V       | OUT  | +5V   | 5V 输出   |
  | 2        | PPM_IN   | IN   | +3.3V | PPM 输入  |
  | 3        | RSSI_IN  | IN   | +3.3V | RSSI 输入 |
  | 4        | FAN_OUT  | OUT  | +5V   | 风扇输出  |
  | 5        | SBUS_OUT | OUT  | +3.3V | SBUS 输出 |
  | 6        | GND      | 接地 |       |           |

- **FMU SD 卡 - microSD**

### 右侧

![Right side](../../assets/flight_controller/airlink/airlink-interfaces-right.jpg)

- **右侧接口：**

  - 带电源输出的以太网端口
  - 遥测端口
  - 第二个 GPS 端口
  - 备用 I2C / UART 端口
  - 飞行控制器 USB Type-C
  - Micro SIM 卡
  - HDMI 输入端口（载荷摄像头）

- **以太网 - JST GH SM08B-GHS-TB**

  | 引脚编号 | 引脚名称 | 方向 | 电压  | 功能           |
  | -------- | -------- | ---- | ----- | -------------- |
  | 1        | 5V       | OUT  | +5V   | 无线电模块电源 |
  | 2        | 5V       | OUT  | +5V   | 无线电模块电源 |
  | 3        | ETH_TXP  | OUT  | +3.3V | 以太网发送正极 |
  | 4        | ETH_TXN  | OUT  | +3.3V | 以太网发送负极 |
  | 5        | ETH_RXP  | IN   | +3.3V | 以太网接收正极 |
  | 6        | ETH_RXN  | IN   | +3.3V | 以太网接收负极 |
  | 7        | GND      | 接地 |       |                |
  | 8        | GND      | 接地 |       |                |

- **TEL3 - JST GH SM06B-GHS-TB**

  | 引脚编号 | 引脚名称   | 方向 | 电压  | 功能         |
  | -------- | ---------- | ---- | ----- | ------------ |
  | 1        | 5V         | OUT  | +5V   | 电源输出     |
  | 2        | USART2_TX  | OUT  | +3.3V | 遥测 3 TX    |
  | 3        | USART2_RX  | IN   | +3.3V | 遥测 3 RX    |
  | 4        | USART2_CTS | IN   | +3.3V | 遥测 3 CTS   |
  | 5        | USART2_RTS | OUT  | +3.3V | 遥测 3 RTS   |
  | 6        | GND        | 接地 |       |              |

- **I2C3 / UART4 - JST GH SM06B-GHS-TB**

  | 引脚编号 | 引脚名称  | 方向 | 电压  | 功能         |
  | -------- | --------- | ---- | ----- | ------------ |
  | 1        | 5V        | OUT  | +5V   | 电源输出     |
  | 2        | USART4_TX | OUT  | +3.3V | UART 4 TX    |
  | 3        | USART4_RX | IN   | +3.3V | UART 4 RX    |
  | 4        | I2C3_SCL  | I/O  | +3.3V | I2C3 时钟    |
  | 5        | I2C3_SDA  | I/O  | +3.3V | I2C3 数据    |
  | 6        | GND       | 接地 |       |              |

- **GPS2 - JST GH SM06B-GHS-TB**

  | 引脚编号 | 引脚名称  | 方向 | 电压  | 功能         |
  | -------- | --------- | ---- | ----- | ------------ |
  | 1        | 5V        | OUT  | +5V   | 电源输出     |
  | 2        | USART8_TX | OUT  | +3.3V | UART 8 TX    |
  | 3        | USART8_RX | IN   | +3.3V | UART 8 RX    |
  | 4        | I2C2_SCL  | I/O  | +3.3V | I2C2 时钟    |
  | 5        | I2C2_SDA  | I/O  | +3.3V | I2C2 数据    |
  | 6        | GND       | 接地 |       |              |

- **FMU USB - USB Type C**
- **SIM 卡 - micro SIM**
- **HDMI - mini HDMI**

### 前侧

![Front side](../../assets/flight_controller/airlink/airlink-interfaces-front.jpg)

- **前侧接口：**

  - 主 GNSS 和指南针端口
  - 主遥测端口
  - CSI 摄像头输入
  - CAN 1
  - CAN 2

- **TEL1 - JST GH SM06B-GHS-TB**

  | 引脚编号 | 引脚名称   | 方向 | 电压  | 功能         |
  | -------- | ---------- | ---- | ----- | ------------ |
  | 1        | 5V         | OUT  | +5V   | 电源输出     |
  | 2        | USART7_TX  | OUT  | +3.3V | 遥测 1 TX    |
  | 3        | USART7_RX  | IN   | +3.3V | 遥测 1 RX    |
  | 4        | USART7_CTS | IN   | +3.3V | 遥测 1 CTS   |
  | 5        | USART7_RTS | OUT  | +3.3V | 遥测 1 RTS   |
  | 6        | GND        | 接地 |       |              |

- **GPS1 - JST GH SM10B-GHS-TB**

  | 引脚编号 | 引脚名称   | 方向 | 电压  | 功能         |
  | -------- | ---------- | ---- | ----- | ------------ |
  | 1        | 5V         | OUT  | +5V   | 电源输出     |
  | 2        | USART1_TX  | OUT  | +3.3V | GPS 1 TX     |
  | 3        | USART1_RX  | IN   | +3.3V | GPS 1 RX     |
  | 4        | I2C1_SCL   | I/O  | +3.3V | 磁力计 1 时钟|
  | 5        | I2C1_SDA   | I/O  | +3.3V | 磁力计 1 数据|
  | 6        | SAFETY_BTN | IN   | +3.3V | 安全按钮     |
  | 7        | SAFETY_LED | OUT  | +3.3V | 安全 LED     |
  | 8        | +3V3       | OUT  | +3.3V | 3.3V 输出    |
  | 9        | BUZZER     | OUT  | +5V   | 蜂鸣器输出   |
  | 10       | GND        | 接地 |       |              |

- **CAN1 - JST GH SM04B-GHS-TB**

  | 引脚编号 | 引脚名称 | 方向 | 电压 | 功能              |
  | -------- | -------- | ---- | ---- | ----------------- |
  | 1        | 5V       | OUT  | +5V  | 电源输出          |
  | 2        | CAN1_H   | I/O  | +5V  | CAN 1 高 (120Ω)  |
  | 3        | CAN1_L   | I/O  | +5V  | CAN 1 低 (120Ω)  |
  | 4        | GND      | 接地 |      |                   |

- **CAN2 - JST GH SM04B-GHS-TB**

  | 引脚编号 | 引脚名称 | 方向 | 电压 | 功能              |
  | -------- | -------- | ---- | ---- | ----------------- |
  | 1        | 5V       | OUT  | +5V  | 电源输出          |
  | 2        | CAN2_H   | I/O  | +5V  | CAN 2 高 (120Ω)  |
  | 3        | CAN2_L   | I/O  | +5V  | CAN 2 低 (120Ω)  |
  | 4        | GND      | 接地 |      |                   |

- **摄像头 - FPC 30 针，0.5mm 间距**

### 后侧

![Back side](../../assets/flight_controller/airlink/airlink-interfaces-back.jpg)

- **后侧接口：**

  - SBUS 输入
  - 16个 PWM 输出通道
  - 2个 LTE 天线接口（MIMO）
  - WiFi 天线接口（AP 和站点模式）

# 串行映射

AIRLink 具有大量内部和外部串行端口：

| 串行     | UART    | 功能                          |
| -------- | ------- | ----------------------------- |
| Serial 0 | USB     | 控制台                        |
| Serial 1 | UART 7  | 遥测 1                        |
| Serial 2 | UART 5  | 遥测 2（与任务计算机内部使用）|
| Serial 3 | USART 1 | GPS 1                         |
| Serial 4 | UART 8  | GPS 2                         |
| Serial 5 | USART 3 | 调试控制台（内部连接器）      |
| Serial 6 | USART 2 | 遥测 3                        |
| Serial 7 | UART 4  | 外部 UART                     |

## RC 输入

RC 输入配置在 SBUS 引脚上，通过内部逆变器连接到 IO MCU。
对于 PPM 接收器，请使用位于设备左侧的 RC 连接器 PPM 引脚。

![RC Input](../../assets/flight_controller/airlink/airlink-rc-input.jpg)

## 输出

AIRLink 有 16 个 PWM 输出。主输出 1-8 连接到 IO MCU。辅助输出 1-8 连接到 FMU。

| 输出   | 定时器   | 通道      |
| ------ | -------- | --------- |
| AUX 1  | Timer 1  | Channel 4 |
| AUX 2  | Timer 1  | Channel 3 |
| AUX 3  | Timer 1  | Channel 2 |
| AUX 4  | Timer 1  | Channel 1 |
| AUX 5  | Timer 4  | Channel 2 |
| AUX 6  | Timer 4  | Channel 3 |
| AUX 7  | Timer 12 | Channel 1 |
| AUX 8  | Timer 12 | Channel 2 |

[DShot](../peripherals/dshot.md) 可以在前四个 AUX 引脚上使用。

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，_QGroundControl_ 会自动安装。
:::

要为此目标[构建 PX4](../dev_setup/building_px4.md)：

```
make sky-drones_smartap-airlink
```

## 外设

- [SmartAP GPS](../gps_compass/gps_smartap.md) - 带指南针、压力传感器和 RGB LED 的 GPS 模块
- [SmartAP PDB](../power_module/sky-drones_smartap-pdb.md) - 电源分配板

## 参考设计

![Reference design](../../assets/flight_controller/airlink/airlink-reference-design.png)

AIRLink CAD 模型可在[此处](https://docs.sky-drones.com/airlink/cad-model)获得

AIRLink 参考设计可根据要求提供。
请通过 [Sky-Drones 联系页面](https://sky-drones.com/contact-us)联系我们

## 更多信息

有关设置和使用 AIRLink 系统的更多信息和说明，请参阅 [AIRLink 文档](https://docs.sky-drones.com/airlink/)。

如需技术帮助、支持和定制，请通过 [Sky-Drones 联系页面](https://sky-drones.com/contact-us)联系我们。

更多信息可在 [www.sky-drones.com](https://sky-drones.com) 找到。

常见问题在 [FAQ](https://docs.sky-drones.com/airlink/faq) 中得到解答。

## 有用链接

- [AIRLink 产品页面](https://sky-drones.com/airlink)
- [AIRLink 文档](https://docs.sky-drones.com/avionics/airlink)
- [AIRLink 数据表](https://3182378893-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MTMlWysgDtJq8Hid1v7%2Fuploads%2F8AiuNNSwLYnZSscj7uIV%2FAIRLink-Datasheet.pdf?alt=media&token=cbf0c4bf-9ab1-40c5-a0af-c6babdddb690)
- [购买 AIRLink Enterprise 4G](https://sky-drones.com/sets/airlink-enterprise-set.html)
- [购买 AIRLink Enterprise 5G](https://sky-drones.com/sets/airlink-5g-enterprise-set.html)
- [购买 AIRLink Core 4G](https://sky-drones.com/autopilots/airlink-core.html)
- [购买 AIRLink Core 5G](https://sky-drones.com/store/airlink-5g-core.html)
