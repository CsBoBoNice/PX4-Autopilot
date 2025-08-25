# RaccoonLab FMUv6X 自动驾驶仪

:::warning
PX4 不制造此（或任何）自动驾驶仪。
如有硬件支持或合规问题，请联系[制造商](https://raccoonlab.co)。
:::

[RaccoonLab FMUv6X](https://docs.raccoonlab.co/guide/autopilot/RCLv6X.html) 飞控基于以下 Pixhawk​® 标准：[Pixhawk 自动驾驶仪 FMUv6X 标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-012%20Pixhawk%20Autopilot%20v6X%20Standard.pdf)、[自动驾驶仪总线标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf) 和 [连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)。

配备高性能 H7 处理器、模块化设计、三重冗余、温控 IMU 板和隔离传感器域，提供卓越的性能、可靠性和灵活性。
在 RaccoonLab，我们专注于基于 DroneCAN 和 Cyphal 的机载控制系统总线。
我们的自动驾驶仪是更大的 DroneCAN 和 Cyphal 生态系统的一部分，使其成为下一代智能载具的理想选择。

![RaccoonLab FMUv6X](../../assets/flight_controller/raccoonlab/fmuv6x.png)

RaccoonLab 为 Raspberry Pi 和 NVIDIA Jetson Xavier NX 提供多功能 HAT，增强连接性和功能。
[Jetson Xavier NX HAT](https://docs.raccoonlab.co/guide/nx_hat/) 旨在将 CAN 总线与 Jetson Xavier NX 集成，实现对 Cyphal 和 DroneCAN 协议的访问。
[Raspberry Pi CM4 HAT](https://docs.raccoonlab.co/guide/rpi_hat/) 提供强大功能，包括 CAN 总线连接、LTE 调制解调器、内部电压测量、其他 MCU 的 SWD 调试以及通过 MAVLINK 与 PX4 的 UART 通信。
这些 HAT 扩展了设备的能力，使它们成为高级机器人和无人机应用的理想选择。

:::tip
此自动驾驶仪[受到](../flight_controller/autopilot_pixhawk_standard.md) PX4 维护和测试团队的支持。
:::

## 关键设计要点

- 高性能 STM32H753 处理器
- 模块化飞控：分离的 IMU、FMU 和基板系统，通过 100 针和 50 针 Pixhawk 自动驾驶仪总线连接器连接。
- 冗余：3x IMU 传感器和 2x 气压计传感器在独立总线上
- 三重冗余域：完全隔离的传感器域，具有独立总线和独立电源控制
- 新设计的减振系统，过滤高频振动并降低噪声，确保准确读数
- 以太网接口，用于高速任务计算机集成

## 处理器和传感器

- FMU 处理器：STM32H753
  - 32 位 Arm Cortex-M7，480MHz，2MB 闪存，1MB RAM
- IO 处理器：STM32F100
  - 32 位 Arm Cortex-M3，24MHz，8KB SRAM
- 板载传感器
  - 加速度计/陀螺仪：ICM-20649 或 BMI088
  - 加速度计/陀螺仪：ICM-42688-P
  - 加速度计/陀螺仪：ICM-42670-P
  - 磁力计：BMM150
  - 气压计：2x BMP388

## 电气数据

- 电压规格：
  - 最大输入电压：36V
  - USB 电源输入：4.75~5.25V
  - 舵机导轨输入：0~36V
- 电流规格：
  - `TELEM1` 输出电流限制器：1.5A
  - 所有其他端口组合输出电流限制器：1.5A

## 机械数据

- 尺寸
  - 飞控模块：38.8 x 31.8 x 14.6mm
  - 标准底板：52.4 x 103.4 x 16.7mm
  - 迷你底板：43.4 x 72.8 x 14.2 mm
- 重量
  - 飞控模块：23g
  - 标准底板：51g
  - 迷你底板：26.5g

3D 模型可在 [GrabCAD](https://grabcad.com/library/raccoonlab-autopilot-1) 下载。

![RaccoonLab FMUv6X 工程图](../../assets/flight_controller/raccoonlab/fmuv6x-drw.png)

## 接口

- 16 个 PWM 舵机输出
- Spektrum / DSM 遥控输入
- PPM 和 S.Bus 输入的专用遥控输入
- 专用模拟 / PWM RSSI 输入和 S.Bus 输出
- 4 个通用串口
  - 3 个具有完整流控制
  - 1 个具有独立 1.5A 电流限制 (`TELEM1`)
  - 1 个具有 I2C 和外部 NFC 读取器的额外 GPIO 线路
- 2 个 GPS 端口
  - 1 个完整 GPS 加安全开关端口
  - 1 个基本 GPS 端口
- 1 个 I2C 端口
- 1 个以太网端口
  - 无变压器应用
  - 100Mbps
- 1 个 SPI 总线
  - 2 条芯片选择线
  - 2 条数据就绪线
  - 1 条 SPI SYNC 线
  - 1 条 SPI 复位线
- 2 个 CAN 总线用于 CAN 外设
  - CAN 总线具有独立静默控制或 ESC RX-MUX 控制
- 2 个带 SMBus 的电源输入端口
  - 1 个 AD & IO 端口
  - 2 个额外模拟输入
  - 1 个 PWM/捕获输入
  - 2 条专用调试和 GPIO 线路

## 串口映射

| UART   | 设备     | 端口          |
| ------ | ---------- | ------------- |
| USART1 | /dev/ttyS0 | GPS           |
| USART2 | /dev/ttyS1 | TELEM3        |
| USART3 | /dev/ttyS2 | 调试控制台 |
| UART4  | /dev/ttyS3 | UART4 & I2C   |
| UART5  | /dev/ttyS4 | TELEM2        |
| USART6 | /dev/ttyS5 | PX4IO/RC      |
| UART7  | /dev/ttyS6 | TELEM1        |
| UART8  | /dev/ttyS7 | GPS2          |

## 电压规格

如果提供三个电源，_RaccoonLab FMUv6X_ 可以在电源供应上实现三重冗余。
三个电源导轨是：**POWER1**、**POWER2** 和 **USB**。
RaccoonLab FMUv6X 上的 **POWER1** 和 **POWER2** 端口使用 6 电路 [2.00mm 间距 CLIK-Mate 线对板 PCB 插座](https://www.molex.com/en-us/products/part-detail/5024430670)。

**正常操作最大额定值**

在这些条件下，所有电源将按以下顺序用于为系统供电：

1. **POWER1** 和 **POWER2** 输入（4.9V 至 5.5V）
2. **USB** 输入（4.75V 至 5.25V）

:::tip
制造商 [RaccoonLab 文档](https://docs.raccoonlab.co/guide/autopilot/RCLv6X.html) 是 RaccoonLab FMUv6X 自动驾驶仪的权威参考。
由于它们包含最完整和最新的信息，应优先使用它们。
:::

## 购买渠道

[RaccoonLab 商店](https://raccoonlab.co/store)

[Cyphal 商店](https://cyphal.store)

## 构建固件

:::tip
大多数用户不需要构建此固件！
它是预构建的，当连接适当的硬件时，_QGroundControl_ 会自动安装。
:::

为此目标[构建 PX4](../dev_setup/building_px4.md)：

```sh
make px4_fmu-v6x_default
```

## 支持的平台/机架

任何可以用普通 RC 舵机或 Futaba S-Bus 舵机控制的多轴飞行器/飞机/地面车辆或船只。
完整的支持配置集合可在[机架参考](../airframes/airframe_reference.md)中查看。

## 更多信息

- [Pixhawk 自动驾驶仪 FMUv6X 标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-012%20Pixhawk%20Autopilot%20v6X%20Standard.pdf)
- [Pixhawk 自动驾驶仪总线标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf)
- [Pixhawk 连接器标准](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf)
- [RaccoonLab 文档](https://docs.raccoonlab.co/)
