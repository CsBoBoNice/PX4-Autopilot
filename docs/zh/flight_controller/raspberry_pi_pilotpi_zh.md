# RPi PilotPi 扩展板

<LinkedBadge type="warning" text="实验性" url="../flight_controller/autopilot_experimental.html"/>

:::warning
PX4 不制造此（或任何）自动驾驶仪。
如有硬件支持或合规问题，请联系[制造商](mailto:lhf2613@gmail.com)。
:::

_PilotPi_ 扩展板是一个功能完整的解决方案，可直接在 Raspberry Pi 上运行 PX4 自动驾驶仪。
它被设计为一个低成本但高度可扩展的平台，可从 Linux 和 PX4 两侧持续更新。
不需要专有驱动程序，因为所有组件都有来自 RPi 和 PX4 社区的上游支持。
PCB 和原理图也是开源的。

![配备 RPi 4B 的 PilotPi](../../assets/flight_controller/pilotpi/hardware-pilotpi4b.png)

## 快速摘要

- 支持的 RPi 板：
  - Raspberry Pi 2B/3B/3B+/4B
- 支持的操作系统：
  - Raspberry Pi OS
  - Ubuntu Server (armhf/arm64)
- 加速度计/陀螺仪：
  - ICM42688P
- 磁力计：
  - IST8310
- 气压计：
  - MS5611
- PWM：
  - PCA9685
- ADC：
  - ADS1115
- 电源：
  - 3~6S 电池，内置电压检测。
  - 通过 USB 线缆为 Pi 供电
- 可用性：_准备发货_

## 连接性

扩展板提供：

- 16x PWM 输出通道
- GPS 连接器
- 数传连接器
- 外部 I2C 总线连接器（**注意：** 与 CSI 摄像头冲突）
- 遥控输入端口 (SBUS)
- 3x ADC 通道，范围 0~5V
- 2*8 2.54mm 未使用的 GPIO 连接器

从 RPi 直接访问：

- 4x USB 连接器
- CSI 连接器（**注意：** 与外部 I2C 总线冲突）
- 等等。

## 推荐接线

![PilotPi 电源部分接线](../../assets/flight_controller/pilotpi/pilotpi_pwr_wiring.png)

![PilotPi 传感器部分接线](../../assets/flight_controller/pilotpi/pilotpi_sens_wiring.png)

## 引脚图

:::warning
它仍然使用旧的 GH1.25 连接器。
接线与 Pixhawk 2.4.8 兼容
:::

### 连接器

#### GPS 连接器

映射到 `/dev/ttySC0`

| 引脚 | 信号 | 电压 |
| --- | ------ | ---- |
| 1   | VCC    | +5V  |
| 2   | TX     | +3v3 |
| 3   | RX     | +3v3 |
| 4   | NC     | +3v3 |
| 5   | NC     | +3v3 |
| 6   | GND    | GND  |

#### 数传连接器

映射到 `/dev/ttySC1`

| 引脚 | 信号 | 电压 |
| --- | ------ | ---- |
| 1   | VCC    | +5V  |
| 2   | TX     | +3v3 |
| 3   | RX     | +3v3 |
| 4   | CTS    | +3v3 |
| 5   | RTS    | +3v3 |
| 6   | GND    | GND  |

#### 外部 I2C 连接器

映射到 `/dev/i2c-0`

| 引脚 | 信号 | 电压          |
| --- | ------ | ------------- |
| 1   | VCC    | +5V           |
| 2   | SCL    | +3v3(上拉) |
| 3   | SDA    | +3v3(上拉) |
| 4   | GND    | GND           |

#### RC 和 ADC2/3/4

RC 映射到 `/dev/ttyAMA0`，RX 线路上有信号反相器开关。

| 引脚 | 信号 | 电压     |
| --- | ------ | -------- |
| 1   | RC     | +3V3~+5V |
| 2   | VCC    | +5V      |
| 3   | GND    | GND      |

- ADC1 内部连接到分压器用于电池电压监测。
- ADC2 未使用。
- ADC3 可以连接到模拟空速传感器。
- ADC4 在 ADC 和 VCC 之间有一个跳线帽，用于监测系统电压水平。

| 引脚 | 信号 | 电压   |
| --- | ------ | ------ |
| 1   | ADCx   | 0V~+5V |
| 2   | VCC    | +5V    |
| 3   | GND    | GND    |

::: info
ADC3 和 4 有另一个 VCC 源
当 'Vref' 开关打开时，'VCC' 引脚由 REF5050 驱动。
:::

#### 板顶部未使用的 GPIO

| 扩展板引脚 | BCM | WiringPi | RPi 引脚 |
| ---------- | --- | -------- | ------- |
| 1          | 3V3 | 3v3      | 3V3     |
| 2          | 5V  | 5V       | 5V      |
| 3          | 4   | 7        | 7       |
| 4          | 14  | 15       | 8       |
| 5          | 17  | 0        | 11      |
| 6          | 27  | 2        | 13      |
| 7          | 22  | 3        | 15      |
| 8          | 23  | 4        | 16      |
| 9          | 7   | 11       | 26      |
| 10         | 5   | 21       | 29      |
| 11         | 6   | 22       | 31      |
| 12         | 12  | 26       | 32      |
| 13         | 13  | 23       | 33      |
| 14         | 16  | 27       | 36      |
| 15         | 26  | 25       | 37      |
| 16         | GND | GND      | GND     |

### 开关

#### RC 反相器

此开关将决定 RX 线路的信号极性：`UART_RX = SW xor RC_INPUT`

- 开：适用于 SBUS（信号反相）
- 关：保留

#### Vref

ADC 3 和 4 的 VCC 将由以下驱动：

- 如果打开，由 REF5050 输出 Vref
- 如果关闭，直接从 RPi 的 5V 引脚

#### 启动模式

此开关连接到 Pin22(BCM25)。
系统 rc 脚本将检查其值并决定 PX4 是否应与系统启动一起启动。

- 开：自动启动 PX4
- 关：不启动 PX4

## 开发者快速入门

请参考您的 RPi 上运行的操作系统的具体说明：

- [Raspberry Pi OS Lite (armhf)](raspberry_pi_pilotpi_rpios.md)
- [Ubuntu Server (arm64 & armhf)](raspberry_pi_pilotpi_ubuntu_server.md)
